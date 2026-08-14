---
type: note
description: >-
  Статус Google-инструментов на сервере: gws (Google Workspace CLI) не авторизован, Antigravity CLI сломан (переустановка + OAuth); оба ждут решения владельца
tags: [google, cli, tools, setup]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-10
source: "daily/2026-08-10.mdtier: active"
last_accessed: 2026-08-10
tier: active
relevance: 0.925
---

# Google CLI / Antigravity: статус

# Google CLI / Antigravity: статус (09.08.2026)

## gws (Google Workspace CLI)
- Установлен, но авторизации НЕТ: ни клиентского ключа, ни токена; в `.env` пусто; кэш — не креды.
- Подключение ~5 мин по скиллу google-workspace: OAuth-клиент в Google Cloud console.
- Нужен для Gmail/Календаря/Drive/Таблиц. Вопрос владельцу «Поднимаем?» — без ответа.

## Antigravity CLI
- Ставился 04.08 внутри Gemini CLI (npm @google/gemini-cli@0.53.1), токен/конфиг остались, запускался (Gemini 3.6 Flash), но бинарник/бандл пропал — остался только webm_encoder.
- Отдельного пакета @google/antigravity-cli нет → переустановка + новый OAuth.
- Упоминание Antigravity 08.08 — новость Пичая про внутреннюю платформу Google, не про сервер.
