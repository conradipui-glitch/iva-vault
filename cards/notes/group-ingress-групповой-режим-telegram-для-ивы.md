---
type: "note"
description: "Патч group-ingress (07.09.2026) добавляет Иве групповой режим Telegram: при TELEGRAM_GROUP_MODE=all группы обрабатываются как личка. Добавлен telegram-group-mode.ts."
tags: ["telegram","group","iva","feature","patch"]
status: "active"
confidence: "EXTRACTED"
domain: "work"
created: "2026-09-08"
source: "daily/2026-09-08.md"
last_accessed: "2026-09-05"
tier: "active"
relevance: 0.895
access_count: 1
---

# group-ingress: групповой режим Telegram для Ивы

Патч от glmbot (Hermes-агент), применён 07.09.2026 поверх рабочей версии. Добавляет Иве групповой режим Telegram: при TELEGRAM_GROUP_MODE=all группы обрабатываются так же, как личка. В патче добавлен агент/lib/telegram-group-mode.ts. Закоммичен в local-ветку (ce8889b, 5 файлов). Тесты telegram-inbound 27/27 и telegram-queue 31/31 прошли. Файлы живут в апстримовском дереве, поэтому при следующем обновлении будут конфликты — предсказуемые, через allowlist.

## Related

- [[cards/notes/провайдер-b-ai-ива]]
- [[cards/projects/гермес-агент-сосед-на-vps]]
- [[cards/projects/_index]]
