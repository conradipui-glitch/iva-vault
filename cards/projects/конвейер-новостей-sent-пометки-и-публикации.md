---
type: project
description: >-
  Рабочий конвейер новостей: хранилище data/news/store.json, статус sent у обработанных, команда iva-news-mark, публикации 05.08.2026 (Apple vs OpenAI, Брэдбери, Xbox)
tags: [news, automation, sent, threads, x]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-06
source: daily/2026-08-06.md
access_count: 1
last_accessed: 2026-06-27
relevance: 0.4
tier: cold
---

# Конвейер новостей: sent-пометки и публикации

# Конвейер новостей: sent-пометки и публикации

## Механика пометок (10:36, 05.08.2026)
- У каждой новости в `data/news/store.json` статус `sent`.
- Все обработанные помечены: Apple vs OpenAI (обе статьи), FFmpeg 9.0, Qwen3.8-Max, SQLite CVE, Kimi K3 (3 вхождения), DeepSeek V4 Flash, humanizer-cli и ещё несколько (итого 13).
- `iva-news` не показывает помеченные: в выдаче 20 из 99 необработанных; яблочная тема и FFmpeg ушли.
- Команды: `iva-news-mark <url или подстрока>` — пометить (можно пачкой), `--unmark` — снять, `--list` — посмотреть, `--clear` — снять всё.
- Правило процесса: как только черновик/пост по теме отправлен, сразу пометить — повторно в выжимке не появится. Новые (WorldCup, ALiBi, Shieldstral) ещё не помечены, пока не отправлены. Предложение: добавить автопометку в скилл news-editor.

## Публикации 05.08.2026
- 01:07 — Apple vs OpenAI (Threads, API, 498 симв., без картинки): https://www.threads.net/@toharo_pro/post/18037256234816385
- 19:30 — Рэй Брэдбери «Будет ласковый дождь»: X https://x.com/TrampampamAGI/status/2084993628808577484 + Threads https://www.threads.com/@toharo_pro/post/DbqP-2YjSTn (с обложкой).
- 19:32 — Xbox офлайн/диски: X https://x.com/TrampampamAGI/status/2084995805006483891 + Threads https://www.threads.com/@toharo_pro/post/DbqQNSKjXKG (одна обложка).
- Брэдбери и Xbox — тексты для площадок разные (X короткий и резкий, Threads развёрнутый).

## Черновики/подготовленные 05.08 (судьба не подтверждена)
- 09:35 — WorldCup Arena, ALiBi, humanizer-cli (JSON-массив).
- 13:01 — OpenAI-побег моделей (пост + image_prompt киберкот-хакер).
- 13:35 — пачка черновиков (JSON, обрезан).
- 21:35 — 3 черновика-мысли: TencentDB Agent Memory, Cloudflare workspace на Workers, iFixAi-проверка агентов.

## Связанные решения
- Посты-мысли/вопросы, без ссылок в финале, человечно, без длинных тире (см. [[cards/projects/threads-личный-аккаунт-про-ии-без-котиков]]).

## Related
- [[cards/projects/конвейер-новостей-для-стрингов-кота-бориса]]
- [[cards/projects/threads-личный-аккаунт-про-ии-без-котиков]]
- [[cards/decisions/x-аккаунт-для-публикаций-стрингов-кота-бориса]]
