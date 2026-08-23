---
type: "note"
description: "Сторож IVA очищен от повторных тревог по историческим сессиям и следит только за активными прогонами."
tags: ["iva","monitoring","telegram","workflow","reliability"]
status: "active"
confidence: "INFERRED"
domain: "knowledge"
created: "2026-08-23"
source: "daily/2026-08-23.md"
last_accessed: "2026-08-23"
tier: "active"
relevance: 0.985
---

# Сторож IVA учитывает только активные прогоны

22.08.2026 сторож каждые пять минут повторно читал исторические записи usage.jsonl, включая отменённые и завершённые сессии, поэтому присылал повторные тревоги.

После исправления он учитывает только прогоны со статусом running и предупреждает один раз на каждые 40 обращений. Старые зависшие прогоны отменены. Первопричиной исторических сессий названы повторные доставки Telegram-моста с устаревшим continuation token и ответом 503. Скрипт перенесён в custom-слой; синтаксис, тестовый и реальный запуск проверены.

## Related

- [[cards/notes/_index]]
- [[cards/notes/curator-infra-iva-systemd]]
- [[cards/decisions/анти-дубль-при-публикации-в-telegram-канал]]
