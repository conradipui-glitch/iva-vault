---
type: note
description: "20.09.2026: Google-генерация мертва — Antigravity отвалился по региону с 19.09, Gemini CLI отправляет в Antigravity; gws по-прежнему не авторизован."
tags: ["google","cli","tools","setup","antigravity","image-generation","pool","ops"]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-10
source: "daily/2026-08-10.mdtier: active"
last_accessed: 2026-08-10
tier: "cold"
relevance: 0.34
updated: "2026-09-21"
---
# Google CLI / Antigravity: статус

Статус Google-инструментов (актуально на 20.09.2026): генерация изображений и текстов через Google мертва. Gemini CLI отвечает «клиент больше не поддерживается, переходите в Antigravity»; сам Antigravity CLI с 19.09.2026 отвалился по региону («not available in your location») — все три модели пула (Opus 4.6 Thinking, Sonnet 4.6, Gemini 3.6) недоступны. Утром 20.09 Antigravity в iva-write вернул пустые ответы. Через Google генерить нечем; картинки решено делать через ChatGPT-подписку (codex). gws (Google Workspace CLI) — по-прежнему без авторизации, решение владельца не получено.

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

## History

- 2026-08-14: Antigravity CLI рабочий (14.08 через него переписана статья Gemini 3.7 Flash); gws не авторизован, решение владельца не получено

## Related

- [[cards/decisions/генератор-обложек-строго-chatgpt-подписка-codex]]
- [[cards/projects/iva-write-пул-исполнителей-подписки]]
- [[MOC/MOC-work|Work]]
