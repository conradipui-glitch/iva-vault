---
tier: "warm"
relevance: 0.685
type: note
description: >-
  Внедрено (10.08.2026, 23:06): vault/raw/ — инбокс для ссылок/статей от владельца; команда «обработай raw» — чтение → карточки → MOC → связи/противоречия. Из практики статьи про Obsidian second brain.
tags: [vault, raw-inbox, workflow, memory]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-10
source: daily/2026-08-10.md
last_accessed: 2026-08-11
---

# raw-инбокс-vault-обработка-входящих

## raw-инбокс (10.08.2026)

Внедрено по итогам разбора статьи про Obsidian second brain (@defileo «Claude + Obsidian should be illegal»): папка `vault/raw/` (README.md создан 10.08 23:06) + команда «обработай raw».

### Что делает
- Владелец кидает ссылку/статью/конспект в чат → Ива складывает в `vault/raw/` и по команде обрабатывает: читает → создаёт карточки → обновляет MOC → показывает связи и противоречия.
- Решает проблему «ссылки оседают в daily-транскрипте и теряются».

### Из той же статьи — что уже было у нас
1. Vault с вики-ссылками + MOC + daily → есть.
2. Промпт «хранителя» (CLAUDE.md) → CORE.md.
3. Ранжированный поиск → memory_search (BM25 + граф).
4. Утренний брифинг cron → morning-digest + окна 07:00/08:00.
5. Ночная обработка daily→weekly→monthly + аудит → ночные rollup'ы + doctor.
6. Транскрипты звонков/голоса → Deepgram в daily.

### Чего не было → взято
- raw-инбокс + команда обработки (сделано).
- Сохранять ценные разборы в cards/notes (частично, сделать правилом).
- Аудит противоречий → предложено добавить шаг в weekly-retro.

### Вердикт по Obsidian
Не нужен: vault живёт на сервере, Obsidian — desktop-окно; «второй мозг» у нас уже есть (на 70–80% реализовано), окно — чат.

## Related
- [[cards/notes/личная-система-памяти-владельца-rig-openmemory-lightrag]]
