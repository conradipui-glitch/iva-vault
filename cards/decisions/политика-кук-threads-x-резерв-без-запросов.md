---
type: decision
description: >-
  Куки Threads и X остаются в резерве, но запросов с них быть не должно нигде (cron, n8n, скрипты) — проверено 06.08.2026
tags: [threads, x, cookies, policy]
status: active
confidence: EXTRACTED
domain: social
created: 2026-08-06
source: daily/2026-08-06.md
last_accessed: 2026-08-07
tier: "cold"
relevance: 0.55
---

# Политика кук Threads/X (резерв, без запросов)

# Политика кук Threads/X — резерв

## Решение (06.08.2026, владелец)
- Куки `threads.env` (браузерные, .threads.com) и `x.env` (TWITTER_AUTH_TOKEN/CT0) **оставить в резерве**.
- **Никаких запросов с этих кук нигде быть не должно**: cron, n8n, скрипты, health-check.
- Threads: только официальный API (`/usr/local/bin/iva-threads-api-post`, токен threads-api.env).
- X: заморожен полностью (бан, см. карточку X-аккаунта).

## Что проверено (06.08.2026)
- crontab: x-auto-post, x-weekly-report, threads-monitor — закомментированы.
- iva-x-reader-gateway.service — отключён.
- health-watch.sh — cookie-блок вырезан.
- n8n — активных воркфлоу с X/Threads нет, кредов нет.
- ai-social-monitor — не запущен, токены пусты.
- Скрипты iva-posts-sync, iva-news-auto — запросов с кук нет.

## На будущее
- Возврат X-автоматики — только после разблокировки аккаунта и решения владельца.
- Threads-монитор (threads-monitor.sh) — вернуть через API, не через куки.

## Related
- [[cards/projects/x-source-watchlist.md]]
