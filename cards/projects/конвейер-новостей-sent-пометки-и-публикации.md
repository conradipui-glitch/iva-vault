---
type: project
description: >-
  Конвейер AI-новостей → черновики → Telegram (канал Стринги кота Бориса) + Threads API; правило: ссылка на репу встраивается в ключевое слово поста; с 09.08 обложки — в вайбе канала (кот Борис)
tags: [news, automation, sent, threads, x, conveyor, telegram, publishing, pollinations, boris]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-06
source: daily/2026-08-06.md
access_count: 4
last_accessed: 2026-08-09
relevance: 0.994
tier: active
updated: 2026-08-10
---

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
- [[cards/decisions/финальный-формат-постов-стрингов-кота-бориса]]
- [[cards/notes/ежедневный-ритм-новостного-канала]]
- [[cards/decisions/обложки-вайб-канала-кот-борис]]
## History

- 2026-08-06: в теле был дубль H1 «Конвейер новостей: sent-пометки и публикации» — свёрнут в один заголовок.

## Log
- 2026-08-07: 06.08.2026: **Набор А** (RealReplicaBench, Prime Agent, Cloudflare OS) — Telegram все 3, Threads посты 1+2 (пост 2 вышел сразу, не через 30 мин — отклонение от тайминга). **Набор Б** (OpenAI безлимит, GPT-5.6 Sol, Kimi K3, CRM-агент, Argus) — Telegram все 5, Threads 3 в очереди на 00:11/00:41/01:11. **Новое правило публикации: ссылка на репу встраивается в ключевое слово** («[Вышел open-source](github.com/...)») — записано в EDITORIAL-STANDARD.md; для Threads ссылка просто один раз в тексте. 06.08 правился news-editor (редакционный стандарт). 16:48 выбран «Вариант а» для набора А.
- 2026-08-09: вечерняя публикация (журнал data/journal/2026-08-08-publish-seedance-kimi-gstack.md): Telegram 3 поста — Seedance 2.5 (бесплатные кредиты $5000/33 дня), Kimi K3 (самая крупная открытая модель, ссылка huggingface.co/moonshotai/Kimi-K3), gstack Гэрри Тана (127K★, ссылка github.com/garrytan/gstack); лимит канала превышен на 1 пост осознанно с согласия владельца. Threads 1 пост (Seedance, пост-польза) + комментарий с деталями через --reply-to. Обложки всех постов — бесплатный Pollinations (zimage 1280x720, seed 20260808/20260809/20260810), превью через iva-pollinations-preview. Черновики дня в data/news/captions/ (openai-hf-timeline, deepmind-weathernext, seedance-2.5-credits, kimi-k3-biggest-open, garrytan-gstack, pichai-quotes). Утром (22:14) ушли ещё 2 поста: «OpenAI случайно атаковала Hugging Face» (таймлайн инцидента) и «DeepMind WeatherNext — модель ураганов» (обложки тогда ещё gpt-image-2: 4,36 и 1,09 ₽). Решение 08.08: обложки постов — только бесплатный Pollinations API (ключ в n8n, credential «Pollinations API»), платную iva-image/gpt-image для обложек не использовать; gpt-image остаётся для дизайн/UI-макетов (см. CORE).
- 2026-08-10:
  Публикации 09.08.2026:
  - Утренняя подборка (09:57–09:58): **Claude Code Auto mode → дефолт для Pro/Max/Team с 14 августа** (аудит 720 атак / 0 успешных; Simon Willison скептичен), **OpenAI купила NextSlide** (генерация презентаций; основатель ранее продал Caper AI за $350M), неофициальный **Kimi Slides skill** (GitHub ★1590), **Genesis Open Models Initiative** Минэнерго США (HN ★345), **human-writing** (GitHub ★1992), Google потеряла/вернула ИИ-исследователей (Хабр), **Gemma Translator** (★588), HN-холивар «Код никогда не был сложной частью» (★612).
  - Днём опубликованы посты Claude Code + OpenAI NextSlide с обложками в «кодовом» стиле (серый из кода, солнце/розетка) — **владелец поправил: вайб канала не соблюдён, «там же кот Борис»** (msg 1054).
  - Пересоздание в вайбе канала: обложки с котом Борисом через Pollinations (seeds 202608096/202608097), старые посты удалены владельцем вручную (msg 1061), переопубликовано 20:15 те же тексты «Котятки…»; Threads-версии опубликованы.
  - План на 10.08 (20:15): **useful repos** (human-writing ★2К + gemma-translator ★590), обложка в стиле Бориса, TG + Threads.
  Урок: message_id
  - `scripts/publish-boris-post.sh` не сохраняет message_id (шлёт только «published: <title>») → без id нельзя удалить старый пост через API, только вручную или через userbot. Доработать: сохранять message_id в журнал (`data/journal/<slug>.md` или `data/news/published.json`). Альтернатива — userbot (`iva userbot setup`, QR; TG Premium у владельца ещё 2 года). Вопрос «давай» от владельца — открыт.
- 2026-08-10: Коррекция 09.08 (13:32–13:36): пост от 08.08 про «до $5000 кредитов на 33 дня без лимита» (Higgsfield) признан вводящим в заблуждение — на деле Unlimited-доступ (генерации без списания кредитов на Seedance 2.5 до 33 дней) только на платных тарифах Plus+. Владелец: «Ранее мы выпускали новость про 5000 долларов… вот нету», «думаю, что это ложь». Новость удалена; журнал 2026-08-08-publish-seedance-kimi-gstack.md обновлён. Урок: проверять условия акций до публикации, маркетинговые цифры на веру не брать.
