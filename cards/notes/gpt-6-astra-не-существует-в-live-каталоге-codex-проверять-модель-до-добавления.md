---
type: "note"
description: "Запрос владельца добавить GPT-6 Astra и уровни мышления в web-панель/меню Telegram: модели нет в авторизованном /models каталоге Codex. Модель не добавлялась; урок — проверять через live-каталог до статического добавления."
tags: ["webapp","models","codex","gpt-6-astra","verification"]
status: "active"
confidence: "EXTRACTED"
domain: "work"
created: "2026-09-06"
source: "daily/2026-09-06.md"
last_accessed: "2026-09-03"
tier: "active"
relevance: 0.925
access_count: 1
---

# GPT-6 Astra не существует в live-каталоге Codex — проверять модель до добавления

05.09.2026 владелец попросил добавить в web-панель и меню Telegram модель «GPT-6 Astra» с уровнями мышления. Проверен авторизованный `/models` каталог Codex — совпадений по `gpt-6` / `astra` ноль, модели в API нет. Неподтверждённые правки откачены, резервные копии в `/root/backups`, задача в фабрике помечена заблокированной. Скорее всего, GPT-6 Astra — фейковый анонс либо модель только в интерфейсе ChatGPT и не выведена в Codex/API. Урок: не добавлять модель и уровни мышления в статический каталог web-панели до независимой проверки через аутентифицированный live-/models endpoint; при появлении модели в live-каталоге добавить автоматически вместе с реально поддерживаемыми уровнями.

## Related

- [[cards/notes/_index]]
- [[cards/notes/добавление-модели-solar-pro-4-в-веб-панель]]
- [[cards/notes/исследование-llm-шлюзов-prodex-subrouter-codex-oauth-bright-]]
