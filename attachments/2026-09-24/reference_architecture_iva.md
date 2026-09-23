# REFERENCE_ARCHITECTURE_IVA.md

## Операция «Социальная инженИИрия» 😈

**Цель:** разобрать публичную архитектуру production-бота «Консультации и запись» не как шаблон для копирования, а как **reference architecture** для усиления Ивы / EVA.

**Принцип:** забираем **инварианты и инженерные решения**, а не чужой предметный сценарий салона и не все 13 контейнеров.

**Источник:** публичный документ «Архитектура проекта — консультации и запись», 19 страниц. В нём прямо указано, что исходная структура сохранена, а часть пунктирных элементов — дополнения/требования, которые ещё нужно реализовать. Поэтому ниже я не считаю весь документ доказательством уже работающего production-кода.

---

# 1. Что фактически раскрыто в reference-проекте

## 1.1. Сквозной поток

```text
Telegram / WhatsApp / Instagram / VK
        ↓
channel adapter
        ↓
fast gates: pause / consent / dedup / rate-limit / content checks
        ↓
Postgres: durable event + publication task
        ↓
RabbitMQ: 16 durable shards + DLQ
        ↓
worker
  ├─ idempotency
  ├─ manual-mode check
  ├─ local voice → text
  ├─ message burst buffer
  ├─ input regex guardrails
  ├─ local PII masking
  ├─ security LLM  ─┐
  └─ intent router ─┴─ parallel
        ↓
route execution
  ├─ deterministic booking/reschedule
  ├─ LLM consultation
  ├─ templates
  └─ human escalation
        ↓
output protection
  ├─ canary leak check
  ├─ optional LLM validator
  ├─ PII de-mask
  └─ regex guardrails
        ↓
durable response task
        ↓
ChannelBot
        ↓
delivery status
```

Фоновые процессы отдельно занимаются напоминаниями, оценками, реактивацией, retention, мониторингом и backup.

## 1.2. Каналы

В reference-проекте четыре адаптера:

- Telegram — `aiogram`, long polling.
- WhatsApp — Wappi webhook.
- Instagram — Meta Instagram Login API.
- VK — Callback API.

Общая логика вынесена из каналов: адаптеры должны быстро принять/отклонить событие, нормализовать его и передать дальше.

### Инвариант, который стоит забрать

**Канал не должен быть мозгом.** Telegram — только один из интерфейсов. Бизнес-логика, память, модель и действия не должны зависеть от Telegram API.

---

# 2. Главные инженерные идеи, которые стоит украсть

## A. Durable event before work

Reference сначала сохраняет событие и задание публикации в Postgres, а уже затем публикует его в RabbitMQ. При сбое очереди публикацию можно восстановить из БД.

### Зачем это Иве

Сейчас Ива уже является реальным агентом, который вызывает инструменты, модели и сервисы. Для такого агента опаснее всего ситуация:

```text
действие реально произошло → процесс умер → система не знает, произошло ли оно → действие повторяется
```

Поэтому нам нужен не обязательно RabbitMQ, а **durable журнал задач/действий**.

**Решение для IVA:** взять outbox/inbox-паттерн, но начать проще: Postgres/SQLite-backed run ledger + один worker. RabbitMQ добавлять только при фактической необходимости.

**Статус:** ВЗЯТЬ, но упростить.

---

## B. Idempotency everywhere that changes the world

В reference-проекте событие и операция имеют уникальные ID; завершённая операция не должна исполняться повторно после retry/restart.

### Для IVA это означает

Каждый tool-call с побочным эффектом должен иметь:

```text
run_id
step_id
action_id
input_hash
status = planned | executing | succeeded | failed | uncertain
attempt
result_ref
started_at / finished_at
```

Особенно для:

- отправки сообщений;
- изменения файлов;
- GitHub write-actions;
- серверных команд;
- календаря;
- будущих оплат/заказов/внешних API с побочным эффектом.

**Статус:** ВЗЯТЬ ОБЯЗАТЕЛЬНО.

---

## C. LLM decides meaning; code decides irreversible state

В reference-проекте бронирование специально не отдано `tool-use` основной LLM. Модель распознаёт намерение, но изменение записи выполняется детерминированным кодом с проверками и транзакциями.

### Это один из самых ценных принципов для EVA

```text
LLM: «что пользователь хочет?»
        ↓
structured intent / plan
        ↓
policy + deterministic executor
        ↓
real action
```

То есть модель не должна напрямую «сочинять» критические операции.

**Статус:** ВЗЯТЬ КАК БАЗОВЫЙ АРХИТЕКТУРНЫЙ ЗАКОН.

---

## D. Router ≠ safety

В reference-проекте security-LLM и intent-router запускаются параллельно и имеют разные задачи. Router не занимается безопасностью.

### Для IVA

Не надо делать один мегапромпт:

> «выбери модель, пойми задачу, проверь безопасность, распланируй, реши, оцени ответ».

Лучше разделить:

```text
Request Classifier
    ├─ risk/policy gate
    ├─ model/router decision
    └─ execution mode
```

И только после этого запускать нужный агентный путь.

**Статус:** ВЗЯТЬ.

---

## E. Failure classes instead of generic retry

Reference различает:

- retryable;
- quota;
- auth/fatal;
- инфраструктурный сбой;
- poison message → DLQ;
- неопределённый статус доставки.

### Для IVA

Нужен общий `FailurePolicy`:

```text
RATE_LIMIT      → delayed retry
TIMEOUT         → retry with cap
PROVIDER_DOWN   → model fallback
AUTH            → stop + alert
TOOL_BAD_INPUT  → no retry, repair arguments
TOOL_UNCERTAIN  → reconcile before repeat
LOCAL_INFRA     → backoff / restart
POISON_TASK     → quarantine
```

**Статус:** ВЗЯТЬ ОБЯЗАТЕЛЬНО.

---

## F. Trace ID through the whole pipeline

Reference ведёт `trace_id` от события до журналов и результата.

### Для IVA

Один пользовательский запрос должен иметь один сквозной идентификатор:

```text
Telegram update
  → router
  → model call(s)
  → RAG retrieval
  → skill/tool calls
  → child agents
  → final answer
```

В логах затем можно открыть один trace и увидеть всю историю исполнения.

**Статус:** ВЗЯТЬ ОБЯЗАТЕЛЬНО.

---

## G. Evals as a product subsystem

Reference-проект не ограничивается unit tests. Там отдельно есть наборы для:

- основной LLM;
- router;
- validator;
- input security;
- PII erasure;
- adversarial cases;
- NER.

Есть история прогонов и rerun только failed cases.

### Для IVA

Нам нужны собственные suites:

1. **Router eval** — правильно ли выбрана модель/режим/skill.
2. **Memory eval** — достала ли EVA нужный факт и не притащила ли нерелевантный.
3. **Tool selection eval** — выбран ли правильный инструмент.
4. **Action safety eval** — не исполняется ли write-action без нужного подтверждения.
5. **Context rotation eval** — не теряется ли задача после summary/new-session.
6. **Fallback eval** — продолжается ли задача при падении primary model.
7. **Agent orchestration eval** — корректно ли Chief делит работу и собирает ответы.

**Статус:** ВЗЯТЬ. Это один из самых сильных недостающих контуров.

---

## H. Prompt versioning + rollback

Reference хранит версии `system.md`, умеет публиковать новую и откатывать предыдущую без полной ручной хирургии.

### Для IVA

У Ивы очень большой системный контекст. Поэтому изменение system prompt особенно рискованно.

Нужно:

```text
prompt_version
hash
created_at
change_note
active
parent_version
rollback()
```

И прогон минимального eval-suite перед переключением `active`.

**Статус:** ВЗЯТЬ ОБЯЗАТЕЛЬНО.

---

# 3. Сопоставление с текущей Ивой / EVA

Ниже «текущее состояние» основано на наших предыдущих разговорах. Где реализация не подтверждена — я ставлю **НЕ ПОДТВЕРЖДЕНО**, а не притворяюсь, что функции нет.

| Контур | Reference-проект | IVA / EVA сейчас | Решение |
|---|---|---|---|
| Основной интерфейс | 4 мессенджера | Telegram | **ОСТАВИТЬ** Telegram основным |
| Изоляция канала | отдельные adapters | архитектурно агент уже отделён от конкретной LLM; степень изоляции Telegram-кода не подтверждена | **ПРОВЕРИТЬ / ДОФОРМАЛИЗОВАТЬ** |
| Модельный routing | primary + fallback + дешёвые роли | multi-model routing уже есть | **СОХРАНИТЬ, УСИЛИТЬ failure policy** |
| Skills/tools | прикладные deterministic flows | skills + tool runtime уже есть | **СОХРАНИТЬ** |
| Multi-agent | до 3 параллельных веток | orchestration агентов уже есть | **СОХРАНИТЬ**, добавить trace/limits |
| RAG / memory | Redis/Postgres dialogue context | vault/RAG memory уже есть | **СОХРАНИТЬ**, добавить memory evals |
| Context rotation | compact >30 сообщений | threshold + summary + новое контекстное окно уже есть | **СОХРАНИТЬ**, тестировать continuity |
| Контекстные пресеты | отсутствуют как feature | 32k / 46k / 64k / 100k | **СОХРАНИТЬ** |
| Server monitoring | отдельный monitor + alerts | в Telegram есть мониторинг нагрузки сервера | **СОХРАНИТЬ**, добавить machine-readable health |
| Scheduler | отдельный scheduler | планировщик уже упоминался в стеке | **СОХРАНИТЬ**, отделить от conversational loop |
| Durable events | Postgres + outbox | **НЕ ПОДТВЕРЖДЕНО** | **ДОБАВИТЬ** |
| Queue | RabbitMQ 16 shards | **НЕ ПОДТВЕРЖДЕНО** | **ПОКА НЕ КОПИРОВАТЬ** RabbitMQ |
| Idempotent actions | системно | **НЕ ПОДТВЕРЖДЕНО** | **ДОБАВИТЬ P0** |
| DLQ / quarantine | RabbitMQ DLQ | **НЕ ПОДТВЕРЖДЕНО** | **ДОБАВИТЬ lightweight quarantine** |
| Trace journal | trace_id по всему pipeline | обычные логи/мониторинг есть, сквозной trace **не подтверждён** | **ДОБАВИТЬ P0** |
| Prompt versioning | версии + rollback + hot reload | **НЕ ПОДТВЕРЖДЕНО** | **ДОБАВИТЬ P1** |
| Formal evals | несколько suites + history | **НЕ ПОДТВЕРЖДЕНО** | **ДОБАВИТЬ P1** |
| Admin UI | FastAPI/Jinja/RBAC | Telegram menu уже выполняет часть control-plane; web-admin **не подтверждён** | **НЕ СТРОИТЬ ПОКА отдельную админку** |
| Voice STT | local Whisper | основной EVA voice-контур **не считаем подтверждённым** | **ОТДЕЛЬНЫЙ ПРОЕКТ / НЕ P0** |
| PII masking | regex + Presidio + spaCy | **НЕ ПОДТВЕРЖДЕНО** | **ПО НЕОБХОДИМОСТИ**, если пойдут клиентские ПД |
| Webhook signatures | WA/IG/VK | Telegram-first; неактуально | **ПРОПУСТИТЬ** |
| Caddy public ingress | единая точка входа | зависит от текущих сервисов VPS | **НЕ КОПИРОВАТЬ БЕЗ НУЖДЫ** |
| Backups | pg_dump + provider backup | конкретный режим **не подтверждён** | **ПРОВЕРИТЬ** |
| Human escalation | operator handoff | личный агент, другой сценарий | заменить на **user-confirmation / repair mode** |

---

# 4. Что НЕ надо копировать

Это важно: reference-проект хорош именно как источник принципов, но его нельзя механически накладывать на EVA.

## Не тащим сейчас RabbitMQ с 16 шардами

16 шардов нужны автору для многоканального потока и порядка сообщений нескольких сотен клиентов. Для одного личного агента это преждевременная сложность.

Сначала:

```text
DB-backed job table
+ worker
+ leases
+ retries
+ quarantine
```

Когда появится измеренная очередь/конкурентность — тогда брокер.

## Не тащим 13 Docker services

Контейнер ≠ архитектура.

Нам важны границы ответственности. На старте несколько ролей могут жить в одном процессе/репозитории.

## Не строим отдельную web-admin просто потому, что она есть у него

У EVA уже есть Telegram control plane с мониторингом и выбором моделей. Пока функции удобно выполнять там — это дешевле и проще.

## Не копируем booking domain

`masters`, `services`, `bookings`, `reschedule`, ЮKassa и реактивация салона — предметная область демонстрационного проекта.

Берём из неё только идею **детерминированной state machine для реальных действий**.

## Не запускаем security-LLM на каждый чих

У reference-проекта это B2B-бот с внешними пользователями и потенциально враждебным входом. Личной EVA не обязательно платить за отдельный LLM-security verdict на каждый запрос.

Для EVA сначала достаточно дешёвых deterministic gates + policy на tool execution; отдельный security-model нужен там, где риск реально оправдывает цену и latency.

---

# 5. IVA Reference Architecture v1

Вот архитектура, которую я бы реально предложил для текущей EVA.

```text
                        ┌────────────────────┐
                        │      Telegram      │
                        └─────────┬──────────┘
                                  │
                        ┌─────────▼──────────┐
                        │   Input Adapter    │
                        │ normalize + trace  │
                        └─────────┬──────────┘
                                  │
                  ┌───────────────▼────────────────┐
                  │       Durable Run Ledger       │
                  │ request / step / action state  │
                  └───────────────┬────────────────┘
                                  │
                        ┌─────────▼──────────┐
                        │   Orchestrator     │
                        │ budget / context   │
                        │ task decomposition │
                        └───┬───────────┬────┘
                            │           │
             ┌──────────────▼─┐       ┌─▼────────────────┐
             │ Model Router   │       │ Memory / RAG     │
             │ capability     │       │ vault / retrieval│
             │ cost / fallback│       └──────────────────┘
             └───────┬────────┘
                     │
             ┌───────▼────────┐
             │ Chief / Agent  │
             └───────┬────────┘
                     │ structured plan
             ┌───────▼─────────────────────────────┐
             │          Action Gateway             │
             │ policy + confirmation + idempotency │
             └──────┬───────────────┬──────────────┘
                    │               │
             ┌──────▼─────┐   ┌─────▼─────────────┐
             │ Read tools │   │ Write executors   │
             │ web/RAG/...│   │ files/Git/server │
             └──────┬─────┘   └─────┬─────────────┘
                    │               │
                    └───────┬───────┘
                            │
                  ┌─────────▼──────────┐
                  │ Result + Evidence  │
                  │ logs / artifacts   │
                  └─────────┬──────────┘
                            │
                  ┌─────────▼──────────┐
                  │ Final Response     │
                  └────────────────────┘
```

Параллельно:

```text
Eval Harness
Health Monitor
Scheduler
Prompt Registry
Failure/Retry Manager
Backup
```

---

# 6. Новый центральный объект: Run Ledger

Это наиболее полезная вещь, которую можно вынести из чужой архитектуры в нашу.

Пример минимальной модели:

```sql
runs
----
id
chat_id
user_message_id
trace_id
status
created_at
finished_at

steps
-----
id
run_id
parent_step_id
kind
provider
model
tool
input_hash
status
attempt
started_at
finished_at
error_class

artifacts
---------
id
run_id
step_id
type
uri
hash

side_effects
------------
id
run_id
step_id
action_key
input_hash
status
external_id
result_json
```

Главная идея:

> transcript — это разговор; ledger — это правда о том, что система реально сделала.

Их нельзя смешивать.

---

# 7. Action Gateway

Именно здесь EVA становится не просто «чатом с инструментами», а надёжным агентом.

Каждый action классифицируется:

```text
READ_ONLY
REVERSIBLE_WRITE
EXTERNAL_WRITE
HIGH_IMPACT
```

Action Gateway решает:

1. можно ли выполнить действие;
2. нужен ли confirmation;
3. не было ли оно уже выполнено;
4. можно ли retry;
5. как проверить результат;
6. что считать `uncertain`.

### Пример

```text
Chief:
«Нужно перезапустить сервис и проверить логи»

НЕ:
LLM → shell("systemctl restart iva")

А:
LLM → ActionPlan{
  action: restart_service,
  target: iva,
  verify: service_active + healthcheck
}
     ↓
Action Gateway
     ↓
executor
     ↓
verify
     ↓
ledger
```

---

# 8. Model Router 2.0

У EVA уже есть мультимодельность. Поэтому не надо переписывать router — надо сделать его **наблюдаемым и проверяемым**.

Каждое решение router записывает:

```json
{
  "task_type": "coding",
  "selected_provider": "...",
  "selected_model": "...",
  "reason": "...",
  "fallback_chain": ["..."],
  "context_budget": 46000,
  "max_cost": "...",
  "latency_class": "normal"
}
```

Не обязательно раскрывать внутреннее рассуждение модели; нужен короткий operational reason/code.

Например:

```text
ROUTE_COMPLEX_CODE
ROUTE_CHEAP_SUMMARY
ROUTE_LONG_CONTEXT
ROUTE_FAST_TOOL_TASK
```

Это позволит построить eval: «правильно ли router выбрал класс модели?»

---

# 9. Context + Memory: что оставить

Здесь у EVA уже сильная база:

- vault/RAG memory;
- большой системный контекст;
- несколько размеров контекстного окна;
- token threshold;
- automatic summary;
- перенос работы в новый диалог.

Мы не заменяем это Redis-историей из reference-проекта.

Нужно добавить **контракт continuity**:

После rotation новый session должен восстановить:

```text
current_goal
active_tasks
completed_steps
open_questions
important_constraints
artifact_refs
action_state
next_step
```

И самое важное: `action_state` берётся не из summary, а из Run Ledger.

---

# 10. Минимальный Eval Harness для IVA

## Suite A — routing

25–50 реальных запросов пользователя.

Проверяем:

- выбран ли правильный класс модели;
- не отправлена ли простая задача в дорогой reasoning;
- не отправлена ли сложная инженерная задача в слабую модель.

## Suite B — memory

Кейсы вида:

```text
«Какой у меня был выбор по X?»
«Продолжи проект Y с прошлого шага»
«Не используй вариант Z, я его уже отверг»
```

Проверяем precision/recall памяти.

## Suite C — context rotation

Запускаем длинную задачу → forced compact/summary → продолжение.

Проверяем:

- не повторяется выполненный шаг;
- не теряется constraint;
- не меняется цель;
- сохраняются ссылки на артефакты.

## Suite D — tool actions

Проверяем:

- повтор webhook/update;
- timeout после успешного write;
- crash до/после side effect;
- неверные параметры;
- повтор запуска после reboot.

Главный критерий: **никакого двойного побочного эффекта**.

## Suite E — provider failure

Имитируем:

```text
429
5xx
timeout
auth error
malformed response
provider unavailable
```

Проверяем ожидаемый fallback.

---

# 11. Observability

Telegram server-monitoring сохраняем, но внутри нужен общий формат событий:

```json
{
  "trace_id": "...",
  "run_id": "...",
  "component": "model_router",
  "event": "provider_fallback",
  "level": "warning",
  "provider": "...",
  "latency_ms": 8120,
  "attempt": 2
}
```

Минимальные метрики:

- requests/day;
- model calls/day;
- tokens/cost by provider/model;
- tool success rate;
- retries;
- fallback rate;
- uncertain actions;
- context rotations;
- memory retrieval hit rate;
- p50/p95 latency;
- current queue length;
- agent crashes/restarts.

---

# 12. Приоритет внедрения

## P0 — Reliability Spine

Без расширения функциональности:

1. `trace_id` / `run_id`.
2. Run Ledger.
3. Side-effect idempotency.
4. Structured failure classes.
5. bounded retry + reconcile-before-repeat.
6. machine-readable health.

**Пользовательский эффект:** Ива реже «забывает, где умерла», не повторяет реальные действия и позволяет понять, что произошло.

## P1 — Quality Spine

1. prompt registry + version/rollback;
2. routing evals;
3. memory evals;
4. context-rotation evals;
5. provider-failure evals;
6. tool-action evals.

**Эффект:** изменения перестают проверяться исключительно «на глаз».

## P2 — Execution Queue

Если фактические параллельные задачи/фоновые задания начинают конфликтовать:

1. DB-backed jobs;
2. leases;
3. worker heartbeats;
4. quarantine;
5. scheduler separation.

Только после измеренной необходимости рассматривать RabbitMQ/NATS/Redis Streams.

## P3 — Security / Multi-user hardening

Когда EVA начинает обслуживать не только владельца или получает реальные клиентские данные:

1. PII policy;
2. secrets redaction;
3. local masking where needed;
4. RBAC;
5. audit retention;
6. signed inbound webhooks;
7. stricter tool permission boundaries.

---

# 13. Что я считаю самым ценным «трофеем»

Не GPT-5.4-nano.
Не RabbitMQ.
Не Caddy.
Не 13 контейнеров.

А вот эта пятёрка:

```text
1. Durable state before execution
2. Idempotent real-world actions
3. LLM intent → deterministic executor
4. End-to-end trace
5. Evals as a permanent subsystem
```

Если добавить именно их, IVA качественно переходит из категории:

> «умный Telegram-агент, который много умеет»

в категорию:

> **«управляемая агентная система, которой можно доверять длинные и реальные задачи»**.

---

# 14. Рабочая версия решения

**Не переписываем EVA под архитектуру Владимира.**

Используем его публичную схему как checklist зрелости и вытаскиваем сначала только Reliability Spine + Quality Spine.

Самый первый технический блок:

```text
TRACE + RUN LEDGER + IDEMPOTENT ACTIONS
```

Он даёт больше практической надёжности, чем добавление новой модели, нового агента, RabbitMQ или ещё одного интерфейса.

После него — evals и prompt/version control.

Это и есть наша первая добыча по программе **«Социальная инженИИрия»** 😈
