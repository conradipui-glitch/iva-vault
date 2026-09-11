---
type: note
description: >-
  systemd-run --on-calendar интерпретирует время в TZ сервера (Europe/Amsterdam), а не в Omsk; для публикаций в 20:00 OMSK нужно писать 14:00 UTC. Threads-очередь iva-queue понимает локальное время Omsk (смещение +06).
tags: [telegram, publishing, systemd, timezone, ops]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-16
source: daily/2026-08-16.md
last_accessed: 2026-08-17
tier: "cold"
relevance: 0.61
---

# Таймеры публикации: сервер в Europe/Amsterdam, указывать UTC

16.08.2026 при планировании публикаций: сервер VPS работает в часовом поясе Europe/Amsterdam (CEST, UTC+2), а владелец в Asia/Omsk (UTC+6).

- `systemd-run --user --on-calendar="2026-08-16 20:00:00"` интерпретирует время в TZ сервера → посты уезжали на следующий день. Правильно: `--on-calendar="2026-08-16 14:00:00 UTC"` (20:00 OMSK = 14:00 UTC).
- `iva-queue add --at "20:00"` понимает локальное время Omsk (+06) корректно, т.к. в скрипте есть преобразование (проверено 16.08: задача встала на 14:00 UTC = 20:00 OMSK).

Вывод: для systemd-таймеров всегда указывать явный суффикс UTC; для iva-queue можно писать локальное время Omsk.

## Related

- [[cards/notes/ежедневный-ритм-новостного-канала]]
