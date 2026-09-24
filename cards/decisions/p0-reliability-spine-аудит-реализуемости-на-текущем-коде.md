---
type: "decision"
description: "Аудит 24.09: P0 (trace/Run Ledger/идемпотентность/классификация отказов) реализуем реюзом существующего каркаса; код не писать; patch-set из 5 изменений."
tags: ["reliability","audit","architecture","ops"]
status: "active"
confidence: "EXTRACTED"
domain: "work"
created: "2026-09-25"
source: "daily/2026-09-25.md"
last_accessed: "2026-09-25"
tier: "active"
relevance: 1.0
---

# P0 Reliability Spine: аудит реализуемости на текущем коде

- 2026-09-24, 00:05–00:14: владелец прислал reference-архитектуру (бот записи в салон, 19 стр.) как чек-лист зрелости для Ивы; задача — аудит реализуемости P0 на текущем коде, ничего архитектурно не перестраивать, код не писать до конца аудита.
- Аудит по реальным файлам: durable-ledger уже есть (.eve/.workflow-data, re-enqueue активных прогонов на старте), trace — data/trace (ADR-0010), идемпотентность ответа — telegram-send-once (claim по sessionId+turnId до Bot API), классификация отказов — deliver-policy.ts.
- Не идемпотентны: bash с побочкой, write_file, web-посты через CLI, git-операции, cron-скрипты; единой FailurePolicy для тулов нет; сквозного короткого trace_id нет.
- Чего не делать: RabbitMQ/Postgres/новые сервисы/web-admin; eve не переписывать; SQLite — только поверх, для аналитики, не как новый ledger.
- Минимальный patch-set (5): 1) action-gate.ts — общий claim-хелпер «до действия, по tool+input_hash» (реюз fs-atomic/lease/fail-open); 2) единый failure-policy для тулов по образцу deliver-policy (rate_limit/timeout/auth/bad_input/uncertain/infra); 3) запись того же trace_id из cron-скриптов в data/trace; 4) data/ledger-summary.jsonl — read-only сводка по runs/steps/events; 5) не менять Outbox, security-gate, inbound-пайплайн, model-provider, vault-дейли, provenance/dup-check.
- Статус: аудит завершён, код не тронут; решение о patch-set за владельцем.

## Related

- [[cards/notes/очистка-журналов-eve-и-systemd-workflow-data-journald]]
- [[cards/notes/сторож-iva-учитывает-только-активные-прогоны]]
- [[MOC/MOC-work]]
