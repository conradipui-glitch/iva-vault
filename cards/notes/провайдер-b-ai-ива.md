---
type: "note"
description: "B.AI провайдер подключён к Иве (OpenAI-совместимый, 48 моделей). Патчи bai-provider и group-ingress применены начисто и закоммичены в local-ветку 07.09; MODEL_PROVIDER остался deepseek."
tags: ["bai","provider","api","model","integration"]
status: "active"
confidence: "EXTRACTED"
created: "2026-09-06"
source: "daily/2026-09-06.md"
updated: "2026-09-08"
domain: "knowledge"
last_accessed: "2026-09-08"
tier: "active"
relevance: 0.97
access_count: 1
---

# Провайдер B.AI (Ива)

Провайдер B.AI (OpenAI-совместимый агрегатор, https://api.b.ai/v1, 48 моделей: GPT-5.x, Claude, Gemini, GLM-5.x, DeepSeek, Kimi и др.) подключён к Иве 06.09.2026.

Источник: патч от glmbot (Hermes-агент, /home/hermes-pilot), пакет patches/bai-provider. Плюс владелец подтвердил установку.

Что сделано:
- BAI_API_KEY в .env (взят из /home/hermes-pilot/.hermes/.env, 35 символов).
- Пропатчено 7 файлов: agent/lib/model-provider.ts, agent/provider.ts, scripts/lib/model-catalog.ts, scripts/lib/model-summary.ts, webapp/server.py, scripts/cli/doctor.test.ts, scripts/lib/version-update.test.ts.
- Провайдер gemini (локальная правка Iva от 01.09.2026) сохранён — патч базировался на версии с gemini.
- Мой бэкап це: /root/iva/data/custom/backup-bai-20260906-134255/.
- model-provider.test.ts синхронизирован под добавленный bai (3 списка). Тесты: 127/127 ок, npm run build собран.

Особенности:
- BAI_REASONING_LEVELS — по-модельная матрица уровней в agent/provider.ts (glm-5.3-flash не поддерживает minimal/xhigh; gpt-5.2/5.5 не поддерживает max; claude-sonnet/opus-5 не поддерживает minimal).
- baiFetch — reasoning_effort встраивается в тело запроса (как у RouterAI), совместимого поля eve нет (compatibleReasoning: false).
- Зрение: deepseek-v4-flash-vision-exp (проверено, отвечает на картинку).
- Live-проверка ключа 06.09.2026: GET /models → 200, chat/completions glm-5.3-flash → 200 с reasoning_content.

ВАЖНО: изменения вступают в силу только после перезапуска процесса. Рестарт делает владелец (iva restart / /restart), Ива сама себя не перезапускает.

## Log

- 2026-09-07: Дополнение (вечер 06.09.2026): после рестарта панель не показывала B.AI — веб-панель (iva-webapp) запускалась старой версией (процесс от 24 августа), хотя код с bai лежал в webapp/server.py с 05.09; рестарт сервиса исправил отображение. Но при выборе провайдера B.AI и модели в веб-меню модель не выбиралась, а чат переставал отвечать. Разбор обработчика /api/agent: target = prov or provider_now(), и если модель кликается до смены провайдера, каталог берётся текущего контура → 400 «модели нет в списке». При смене модели вызывается только `systemctl restart iva.service`, а iva-telegram-poll.service — нет, поэтому при зависании агента на старте канал молчит. Пара glm-5.3-flash + max валидна (API отвечает, tool calling работает), но по usage.jsonl ни одной рабочей записи на bai — фактически B.AI ни разу не отработал. Статическая причина падения iva.service не найдена — нужно живое воспроизведение. Слабые места: рестарт поллинга при смене модели + валидация модели по каталогу текущего контура.
- 2026-09-08:
  07.09.2026 (утро) — применён патч bai-provider (7 файлов) и group-ingress (9 файлов) от glmbot. Снял всё к чистому HEAD, наложил патчи начисто, вернул 13 неконфликтующих локальных файлов из бэкапа. 7 файлов, где владелец тоже работал (provider.ts, model-provider.ts, model-catalog.ts, webapp/server.py, doctor.test.ts, model-summary.ts, version-update.test.ts), оставлены версией glmbot. Ключевой момент: glmbot делал патч поверх рабочей версии владельца, поэтому правки на RouterAI/DeepSeek/Gemini сохранились внутри; возвращать их не нужно. MODEL_PROVIDER остался deepseek, B.AI добавлен как опция в /model и веб-панель.
  
  Закоммичено в local-ветку: bd22aad — B.AI провайдер (15 файлов), ce8889b — group-ingress (5 файлов), c011677 — авторские скрипты (17 файлов, в т.ч. tva-*.py, webapp/server.py, context7.ts, workflow-clean.sh). В tree-allowlist.json добавлено 6 записей с причинами для апстримовских файлов, правит живая фича (telegram-inbound, telegram-queue, model-summary, version-update.test и тесты); .state/ маркер добавлен в .gitignore. Полное дерево в бэкапе data/custom/backup-cleanup-20260907-011645/ (36 файлов). Проверки: build exit 0, telegram-inbound 27/27, telegram-queue 31/31, model-provider 26/26, model-catalog 12/12, version-update 67/67, doctor 22/22.
  
  Замечание на будущее: фичи живут в апстримовских файлах (B.AI, group-ingress), поэтому при следующем iva update на них будут конфликты — но предсказуемые, через allowlist.

## Related

- [[cards/projects/гермес-агент-сосед-на-vps]]
- [[cards/projects/_index]]
- [[cards/notes/провайдер-b-ai-ива]]
