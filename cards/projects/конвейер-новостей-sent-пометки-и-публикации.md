---
type: project
description: >-
  Журнал публикаций новостного конвейера (TG/Threads/сайт) и правила. 15.08: опубликован анонс бенчмарка Gemini 3.7 Flash (TG+Threads, обложка bench-gemini-37-approved.png), Notch снят с очереди; правила: анонсы статей сайта — регулярно TG+Threads, в постах обязательны ссылки на продукты/репозитории.
tags: [news, automation, sent, threads, x, conveyor, telegram, publishing, pollinations, boris, pipeline, ai-news]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-06
source: daily/2026-08-06.md
access_count: 4
last_accessed: 2026-08-09
relevance: 0.793
tier: "cold"
updated: "2026-08-21"
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
- [[cards/decisions/решение-правила-контента-котятки-пост-ревью-приоритеты-11-08]]
- [[cards/decisions/x-не-пытаться-постить-только-вручную-владельцем]]
- [[cards/notes/провенанс-постов-модель-специалисты-стоимость-iva-post-provenance]]

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
- 2026-08-12: Публикации 11.08.2026 добавлены: 19:30 Рэй Брэдбери «Будет ласковый дождь» (X https://x.com/TrampampamAGI/status/2084993628808577484 + Threads https://www.threads.com/@toharo_pro/post/DbqP-2YjSTn), 19:32 Xbox офлайн/диски (X https://x.com/TrampampamAGI/status/2084995805006483891 + Threads https://www.threads.com/@toharo_pro/post/DbqQNSKjXKG), 21:47 Водяные знаки Claude + Zoomsday — автопостинг Telegram/Threads, пришли дубли уведомлений (см. анти-дубль, инцидент 11.08). Тексты для площадок разные: X короткий и резкий, Threads развёрнутый.
- 2026-08-13:
  Журнал публикаций конвейера AI-новостей (Telegram @stringikotaborisa / Threads @toharo_pro / сайт toharo-lab) и правила. История — в `## Log` (append-only).
  
  Правила (актуальные): лимит Threads 3 поста в день; Threads-посты ВСЕГДА с обложкой (правило 12.08 после инцидента 14:03: пост #1 тройки вышел текстовым); в TG — вайб кота Бориса, в Threads — обычные обложки, не кот Борис (12.08); X — только вручную владельцем (заблокирован с 06.08); обложки — бесплатный Pollinations для обычных, gpt-image-2/routerai для дизайн-макетов и спец-обложек (Gemini 4 — 1.10₽, Grok 4.6 — 4.41₽).
  
  12.08.2026 публикации:
  - 12:13: пост «shadcn-ui/chatbot-template» (Threads running; TG-версия 718 зн.); лимит Threads 1 из 3.
  - 13:43: инцидент X: задачи `1786515197369`, `1786515209484` упали — `ERROR: файл картинки не найден: /root/iva/data/news/covers/github.com-fca0fea349.png` (обложка-снимок не сохранилась + дубль после рестарта). Потери невелики (X заблокирован).
  - 13:50: тройка в Threads: #1 «Скрытые рассуждения ИИ» → https://www.threads.com/@toharo_pro/post/Db7qmOHDR3k, #2 «Робот-хирург (Surgical WAM)» ~13:49, #3 «Константа Гротендика» ~16:49. X не постила.
  - 13:53: владелец: «В x постить не надо пытаться я сам если или когда восстановлю доступ» → `iva-news-auto.py`: расписание только `threads=+0` (убран `x=+90m`).
  - 20:19–20:37: подборка 5 трендов (huggingface/transformers, llama.cpp/llama.app, WorldClaw tencent-hunyuan.github.io/Hunyuan3D-WorldClaw, ZzzLc0405/photo-abstract-editorial, LinkedIn CringeBot 3000 ▲252) → в TG WorldClaw и CringeBot 3000 (вайб Бориса, обложки кот-геймер/кот-сноб); Threads: https://www.threads.com/@toharo_pro/post/Db8XhAsjTFU и https://www.threads.com/@toharo_pro/post/Db8Xi2sjZJT (оба с картинками).
  - 21:24: Gemini 4 в Threads → https://www.threads.com/@toharo_pro/post/Db8ejH5jbmd: обложка gpt-image-2 «Gemini 4» неон + гем (16:9, 1.10₽), текст «Gemini 4 слили — уже скоро…» (SDK-лик, pre-training, запуск ~конец августа, цели — обойти Claude Fable 5 и GPT-5.6 Sol).
  - 22:06: Grok 4.6 (SpaceXAI) в Threads → https://www.threads.com/@toharo_pro/post/Db8jYE9jaBq: таблица перегенер. gpt-image-2 (тёмный фон, колонка Grok 4.6 High оранжевая, 10 бенчмарков, 4.41₽), текст «Grok 4.6 вышел — передовой интеллект по цене 4.5», лимит Threads ~500–536 зн., store.json помечен как вручную опубликованный, лимит 8/250 за 24ч, в TG не дублировал. Бенчмарки (7 из 10): AA Intelligence Index 61/56/61/62; GDPval-AA v2 1753/1526/1728/1741; CursorBench v3.2 69.9/66.7/67.2/70.5; DeepSWE v1.1 65.9/54/73/70; FrontierCode v1.1 61.3/56.6/60.6/64.9; APEX-Agents 57.5/47.1/56.7/59.2; Terminal-Bench v3.0 26/15.7/34.6/34.1.
- 2026-08-14: 13.08.2026: публикаций не было; подготовлены черновики (4 партии по 3, 09:35/13:35/17:35/21:35): ИИ против программистов середины; Qwen — крупная открытая модель; слабая модель учится у сильной точечно; KADATH — самоэволюция ИИ-агентов (открытый код); anti-slop — набор правил против «почерка нейросети» в коде; GitHub «сначала опиши, потом делай»; локальный ИИ-помощник (без облака); платформа ИИ-кино из текстовой идеи; DeepSeek — открытый инструмент запуска ИИ-агентов (~30k звёзд за сутки, на базе Cordis); Vercel DeepSec — ИИ-агент поиска уязвимостей; DeepSeek собирает из чужих открытых блоков (Cordis).
- 2026-08-15:
  Публикации 14.08.2026:
  - 00:36 — DeepSeek Harness (открытая платформа агентов, ~30k звёзд) и Vercel DeepSec (агент-сканер уязвимостей) — обе в Telegram (вайб Бориса) и Threads; обложки gpt-image-2 (1.95₽ + 0.51₽); 3-я новость Cordis пропущена как дубль (говорит о том же, что 1-я). Журнал и provenance записаны.
  - 19:30/20:00 — GLM-5.3 и разоблачение Claude AI Ultimate (Scam): TG GLM-5.3 — капшн превышал лимит (1832 > 1024 зн.), переписано и опубликовано вручную; Threads ушёл по расписанию 19:30. Scam: TG по расписанию 20:00; Threads блокировала защита («Котятки» в тексте для чужой площадки) — обращение убрано, опубликовано вручную. Провенанс записан, store.json помечен, журнал `2026-08-14-publish-glm53-scam.md` создан. Ссылки: GLM https://www.threads.com/@toharo_pro/post/DcBbIm-Da9j · Scam https://www.threads.com/@toharo_pro/post/DcB0WDzDXKt.
  - 13:27 — владелец предложил добавить к новости про Gemini 3.7 Flash бенчмарк-сравнение на сайте (идея: тестировать модель на типовых задачах, «что там обычно популярно сравнивать»); статус — не реализовано в этот день.
- 2026-08-16:
  Публикации 15.08.2026: анонс бенчмарка Gemini 3.7 Flash — Telegram (канал Бориса, обложка seed 913506, файл data/news/covers/bench-gemini-37-approved.png) и Threads (https://www.threads.com/@toharo_pro/post/DcCwX5RjP9D). Notch снят с очереди публикации, черновики не публиковать.
  
  Правила (заданы владельцем 15.08):
  - Анонсы статей сайта — регулярно и в Telegram, и в Threads: трафик на сайт → в канал (перекрёстная воронка).
  - Если в посте упоминается продукт/репозиторий без введения в контекст — обязательна ссылка: прямая или встроенная в слово, чтобы читатель получил пользу, а не «красивые слова».
- 2026-08-21: 2026-08-20: из 8 черновиков дня (DeepSeek Harness, SondeHub, terminal-code, OpenRouter→Stripe, SPADE, ADEPT, Orchard, GC-OPD) владелец выбрал для Threads №6 ADEPT (с whiteboard-видео), №5 SPADE и №3 terminal-code; три поста встали в очередь на вечернее окно 20:00/21:00/22:00 (пауза ~1 ч, схема 16.08), тексты ≤500 зн. (241/210/221).
