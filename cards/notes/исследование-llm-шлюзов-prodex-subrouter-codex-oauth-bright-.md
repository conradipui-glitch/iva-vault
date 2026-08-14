---
type: note
description: >-
  Ресёрч кандидатов на «сменный LLM backend» (11.08.2026): Prodex — пилот возможен (не drop-in), SubRouter — несовместим, zenith139/codex-oauth — 404, Bright Data CLI — избыточен. На VPS ничего не ставилось.
tags: [llm-gateway, research, codex, deepseek, backend]
status: active
confidence: EXTRACTED
domain: knowledge
created: 2026-08-12
source: daily/2026-08-12.md
last_accessed: 2026-08-14
tier: active
relevance: 0.985
---

# Исследование LLM-шлюзов: Prodex, SubRouter, codex-oauth, Bright Data

11.08.2026, 17:23–18:58: исследование по инициативе владельца — цель «сменный LLM backend» (не менять инфраструктуру, а заменить endpoint на gateway). Повод: ожидаемый рост цен DeepSeek; текущий расход ~50 ₽/день только автоматизации, 100–150 ₽/день при регулярном общении, VPS 1 100 ₽/мес. Требование владельца: ничего не устанавливать на VPS, только анализ исходников и инженерное заключение.

**Prodex** (github.com/christiandoxa/prodex; Rust, 60+ крейтов): multi-account обёртка над Codex CLI, а не универсальный LLM-gateway. Есть DeepSeek-адаптер, quota-мониторинг, rotation профилей, OpenAI-совместимый gateway. Вывод: не drop-in замена — сценарий «DeepSeek + ChatGPT OAuth в одном gateway» не документирован, у eve один MODEL_PROVIDER и мультипровайдерный роутинг из коробки не поддержан. Память/RAG/tools/Telegram живут в eve и от endpoint'а не зависят — при замене не теряются. Рекомендация: сначала проверить — поднять gateway на DeepSeek и прогнать provider.ts через dev-инстанс (фаза 0 не трогает рабочую систему). На VPS ничего не ставилось, только клонирование во временную папку.

**SubRouter** (github.com/manaflow-ai/subrouter; Go, ~99.5k строк, порт 31415): узкий прокси для Codex-подписок (OAuth ChatGPT) + OpenAI/Claude/Kimi/ZAI в формате Responses API (/v1/responses, /v1/messages). /v1/chat/completions отсутствует → с RouterAI/DeepSeek несовместим; для codex-ротации уже есть codex-auth + write-pool → избыточен. Ставить не нужно.

**zenith139/codex-oauth**: репозиторий 404 (пользователь существует, 35 публичных репо, но codex-проекта нет — ссылка удалена/приватна/выдумана). Реальные аналоги: 7shi/codex-oauth (минимальный OAuth-образец для WHAM backend, не production), ndycode/codex-multi-auth (мульти-аккаунт менеджер для Codex CLI).

**Bright Data CLI**: отклонён как избыточный для текущих задач — дорого (оплата за трафик/запрос), контур поиска уже покрыт (web_search/web_fetch/agent-browser/x-reader), лишняя зависимость (npm, API-ключ, биллинг). Вернуться при появлении задачи «спарсить сотни профилей» или площадки с жёстким антиботом (Instagram/FB).

Попутный инцидент 18:44: при закрытии задач исследования случайно закрыта не та задача (астро-финансовые окна, id=15) — восстановлена, все 4 задачи исследования закрыты корректно.

## Related

- [[cards/notes/_index|Knowledge]]
- [[cards/decisions/пилот-явного-prompt-caching-для-iva]]
- [[cards/projects/iva-write-пул-исполнителей-подписки]]
