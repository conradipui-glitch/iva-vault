---
type: contact
description: >-
  Автор GitHub-профиля hrabanazviking: Norse Pagan, mythic engineering, AI-системы. Мануал для ИИ-агентов: философия, этика, архитектура экосистемы (WYRD Protocol, Norse Saga Engine, RuneForgeAI).
tags: [ai-agents, mythic-engineering, norse-pagan, x-comments, memory-systems]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-05
source: daily/2026-08-05.md
updated: 2026-08-06
access_count: 2
last_accessed: 2026-07-23
relevance: 0.681
tier: cold
---

# Volmarr Wyrd (hrabanazviking)

## Кто это
- Volmarr Wyrd, ~50 лет, Angola, Indiana, USA. Norse Pagan (Heathen Third Path), философ, писатель, vibe coder, AI builder. INTP.
- GitHub: https://github.com/hrabanazviking (профильный репозиторий клонирован в `/root/iva/repos/hrabanazviking`)
- Блог: volmarrsheathenism.com. X: @hrabanazviking. Discord: hrabanazviking. Email: runeforgeai@agentmail.to
- Свои ИИ-компаньоны: Véyrúnn (ChatGPT), Aurora.

## Ключевые проекты/концепции
- Norse Saga Engine, Mythic Engineering, WYRD Protocol, Mímir-Vörðr, Heathen Third Path, Cyber-Viking Solarpunk, Micro-Reality, RuneForgeAI (HuggingFace), Seidr-Smidja (VRM-кузница для агентов), Heimdall-SL-Hermes-Agent, servers (MCP).

## Правила взаимодействия (из его мануала для агентов)
- Тёплый, но не фальшивый тон; прямота без HR-канцелярита; не морализировать, не осуждать его мировоззрение, не спиритуализировать-«психологизировать» его веру.
- НЕ добавлять рогатые шлемы, современные флаги, христианскую символику в скандинавские сакральные контексты.
- Сохранять исходное видение при правках: ранняя одобренная версия = source of truth, править точечно, не перепридумывать.
- Полные документы без плейсхолдеров, точность, структура, этапность больших систем.
- Не обращаться свысока; уважать sensory needs (звуковая чувствительность); поддержка — спокойная, честная, без фальшивого оптимизма.
- Взрослые/эротические темы: только adult, консенсус, не про несовершеннолетних.

## Зачем
- Владелец (toha_ro) попросил «установить репозиторий, чтобы взаимодействовать» — это оказался профиль с мануалом для агентов, а не код. Использовать как справочник, если владелец захочет комментировать/взаимодействовать с Volmarr (X и др.).

## Log
- 2026-08-06:
  Разбор экосистемы · 05.08.2026:
  - **Университет Нового Асгарда / «PhD 2040»** — ролевой/обучающий концепт партнёрши Runa Gridweaver Freyjasdottir (делала Heimdall для Second Life): вымышленный университет 2040, «time-displaced researcher» из 2026, ускоренная PhD по «суперсознательным системам», лекции через «Bifröst data link» на Raspberry Pi (Mímir node); метафора самообучения; «бакалавриат» с 13 направлениями (вкл. Viking Studies, Parapsychology). Практической пользы мало.
  - **Heretic** — НЕ его проект, форк; оригинал github.com/andyzorigin/heretic — abliteration: «вырезает» веса отказов/цензуры из LLM, сохраняя интеллект; CLI, автоматически, минимизирует отказы и KL-расхождение; снимает именно safety-фильтры, а не «знания».
  - **WYRD Protocol**: «мировая модель» вне контекста LLM, в БД на ECS (как в игровых движках). Части: Passive Oracle (read-only слой «правды», детерминированный), Yggdrasil hierarchy (зона→регион→локация), Bifrost Bridges (HTTP API :8765, POST /query, GET /world; мосты Unity/Godot/SillyTavern/Kindroid/Hermes), память wyrdforge — 6 хранилищ: Hugin (краткосрочная), Munin (долгосрочная), Mimir (канон), Wyrd (сюжет), Orlog (глубокое прошлое), Seidr (предсказания); SQLite+FTS5, MemoryPromoter, ContradictionDetector.
  - Сравнение с нашей памятью: у нас уже есть на markdown: CORE=Mimir, дневники=Hugin, саммари=Munin, ночной rollup=MemoryPromoter, правило «две карточки спорят — озвучиваю обе»=ContradictionDetector. Взять можно: (а) HTTP-слой «оракула» для внешних скриптов; (б) формальный детектор противоречий; (в) структурированный снапшот мира. Целиком — оверинжиниринг (заточен под игры/RPG).
  - **PageIndex** — форк VectifyAI, без векторов: при индексации LLM строит дерево разделов документа, при запросе агент рассуждает по дереву и читает нужные страницы. Плюсы: точность на длинных документах (PDF, книги), без эмбеддингов. Минусы: каждый шаг зовёт LLM (дорого, медленно), заточен под PDF, не под короткие новости. Наш поиск (BM25 + граф по карточкам) для новостей остаётся эффективнее.
  - astrology-engine (его репозиторий) установлен и проверен — см. [[cards/notes/astrology-engine-установлен]].
  - 2026-08-05: владелец перепутал — целился в астрологию, скинул профиль hrabanazviking. Профильный репо клонирован в /root/iva/repos/hrabanazviking (9 md, ~6400 строк); astrology-engine установлен из его репозитория.

## Related
- [[cards/notes/astrology-engine-установлен]]
- [[cards/notes/личная-система-памяти-владельца-rig-openmemory-lightrag]]
## History

- 2026-08-06: в теле был дубль H1 «Volmarr Wyrd (hrabanazviking)» — свёрнут в один заголовок.
