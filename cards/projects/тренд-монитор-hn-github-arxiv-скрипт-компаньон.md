---
type: project
description: >-
  Скрипт-компаньон собирает свежие AI-тренды из Hacker News, GitHub trending и arXiv, шлёт сигнал в Telegram при >=3 новых и черновики постов-мыслей на одобрение
tags: [news, automation, cron, ai-news, monitoring]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-02
source: daily/2026-08-02.md
last_accessed: 2026-08-04
tier: active
relevance: 0.985
---

# Тренд-монитор HN+GitHub+arXiv (скрипт-компаньон)

# Тренд-монитор HN + GitHub + arXiv (скрипт-компаньон)

## Создан · 2 августа 2026
Владелец попросил добить скрипт-компаньон (обсуждался 1 августа: «оставить Hacker News + GitHub trending + arXiv»).

## Как работает
- Скрипт: `/root/iva/scripts/trends-monitor.mjs`, запуск `node --env-file=.env scripts/trends-monitor.mjs`.
- Собирает БЕЗ LLM (дёшево): HN (Algolia, топ по points за 36ч), GitHub (новые репо за 7 дней, топ по звёздам), arXiv (cs.AI + cs.CL за 72ч — arXiv не публикует по выходным).
- AI-буст: заголовки с AI-словами (ai/llm/agent/model/gpt/claude/openai/anthropic/deepseek/gemini/llama/qwen/kimi/vibe/code/neural/voice/robot) получают +10000 к score — AI-тренды всегда вверху.
- Кросс-дедуп по URL (один проект может выйти и на HN, и в GitHub).
- Дедупликация по state-файлу `/root/.config/iva/trends-state.json` (последние 200 id на источник).
- Сигнал в Telegram ТОЛЬКО при >=3 новых позициях, не чаще 1 раза в 3 часа (cooldown).
- В сигнале: топ-8 свежих трендов + 2–3 черновика постов-мыслей через eve-агента (если доступен) — на одобрение владельцу. Постинг НЕ выполняет.

## Режимы
- `--test` — только сбор, печать в stdout, state не трогает.
- `--force` — сигнал даже если новых <3 (для проверки доставки).

## Cron (активное окно, Amsterdam = Omsk+4)
`35 5,7,9,11,13,15,17 * * *` = 11:35, 13:35, 15:35, 17:35, 19:35, 21:35, 23:35 по Омску.
Лог: `/var/log/trends-monitor.log`.

## Тест · 2 августа 2026
- `--test`: HN=20, GitHub=12, arXiv=12, кросс-дедуп работает.
- `--force`: сигнал с 42 новыми трендами отправлен в Telegram (332664273), черновики подготовлены.
- eve health: HTTP 200 на :8723 — черновики генерируются.

## Related
- [[cards/projects/конвейер-новостей-для-стрингов-кота-бориса]] (источники Superbash/HN/GitHub/arXiv из старых n8n)
- [[cards/projects/threads-личный-аккаунт-про-ии-без-котиков]] (черновики постов-мыслей идут сюда)
