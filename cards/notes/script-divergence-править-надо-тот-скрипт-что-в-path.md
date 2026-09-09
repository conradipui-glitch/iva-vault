---
type: "note"
description: "09.09.2026: два Threads-поста упали, потому что я правил scripts/iva-threads-api-post.py, а /usr/local/bin/iva-threads-api-post (старая копия от 20.08) — вызываемый — не обновлялся. Урок: после правки скрипта проверять установленную копию."
tags: ["ops","scripts","threads","infra","deploy"]
status: "active"
confidence: "EXTRACTED"
created: "2026-09-10"
source: "daily/2026-09-10.md"
updated: "2026-09-10"
domain: "knowledge"
last_accessed: "2026-09-10"
tier: "active"
relevance: 1.0
---

# Script divergence: править надо тот скрипт, что в PATH

09.09.2026: два Threads-поста (Coxon — комментарий, Принтер на e-ink — сам пост) упали с ошибкой «media ID не найден». Первая попытка починить — добавить retry в `scripts/iva-threads-api-post.py` — не сработала: скрипт, который реально вызывается очередью, лежит в `/usr/local/bin/iva-threads-api-post` (копия от 20.08.2026), а правил я `scripts/iva-threads-api-post.py`.

Корень: `threads-post-with-source.sh` запускает `iva-threads-api-post` из PATH, который ведёт в `/usr/local/bin/`. После обновления `scripts/` я не скопировал новый скрипт в `/usr/local/bin/`.

Фикс: скопировал обновлённый скрипт в `/usr/local/bin/iva-threads-api-post`. Проверил остальные скрипты (`iva-queue`, `iva-threads-post`) — они тоже расходятся, но не влияют на работу.

Правило: после правки любого скрипта, вызываемого очередью или cron, проверять его установленную копию в `/usr/local/bin/` (PATH). Либо синхронизировать автоматически.

## Log

- 2026-09-10:
  09.09.2026: два Threads-поста (Coxon — комментарий, Принтер на e-ink — сам пост) упали с ошибкой «media ID не найден». Первая попытка починить — добавить retry в `scripts/iva-threads-api-post.py` — не сработала: скрипт, который реально вызывается очередью, лежит в `/usr/local/bin/iva-threads-api-post` (копия от 20.08.2026), а правил я `scripts/iva-threads-api-post.py`.
  
  Фикс: скопировал обновлённый скрипт с ретраем в `/usr/local/bin/iva-threads-api-post`. После правки любого скрипта, вызываемого очередью или cron, проверять его установленную копию в `/usr/local/bin/`.

## Related

- [[cards/projects/threads-личный-аккаунт-про-ии-без-котиков]]
- [[cards/notes/threads-принимает-обложки-только-jpeg-jpg-png-ошибка-с-ogg-в-image]]
- [[cards/projects/конвейер-новостей-sent-пометки-и-публикации]]
