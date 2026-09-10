---
type: note
description: >-
  Статус Google-инструментов: gws не авторизован (ждёт решения); Antigravity CLI — 14.08.2026 успешно использован: через него написан пост/статья Gemini 3.7 Flash (переписана статья разоблачения), т.е. CLI работает после переустановки.
tags: [google, cli, tools, setup, antigravity]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-10
source: "daily/2026-08-10.mdtier: active"
last_accessed: 2026-08-10
tier: "cold"
relevance: 0.52
updated: 2026-08-15
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

## Log

- 2026-08-15: 14.08.2026: Antigravity CLI снова рабочий — через него Ива переписала статью-разоблачение Claude AI Ultimate через Gemini 3.7 Flash (deploy success). Ранее (09.08) Antigravity CLI был сломан (бинарник/бандл пропал после установки в Gemini CLI), требовал переустановки + нового OAuth. gws (Google Workspace CLI) — по-прежнему без авторизации, решение владельца не получено.
