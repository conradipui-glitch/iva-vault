---
type: decision
description: >-
  Адаптация методологии Garry Tan gstack (Think→Plan→Build→Review→Test→Ship→Reflect) под скиллы Ивы: создан скилл gstack-workflow (data/custom/agent/skills/)
tags: [gstack, methodology, workflow, skill, ai-coding]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-08
source: daily/2026-08-08.md
access_count: 1
last_accessed: 2026-08-08
relevance: 0.79
tier: warm
---

# gstack-workflow — адаптация методологии под Иву

- 2026-08-08: Антон изучил репозиторий Garry Tan gstack (github.com/garrytan/gstack, 127K★, 19.1K форков, 362 коммита, MIT, личный Claude Code-сетап: 23 «специалиста» + 8 power-инструментов, slash-команды на Markdown, темп ~810× от 2013). Решение: НЕ ставить репозиторий как есть (заточен под Claude Code/Bun/свои скрипты), а адаптировать методологию под систему скиллов Ивы.
- Создан скилл `gstack-workflow` в data/custom/agent/skills/ (подхватится после `npm run build` + рестарт): полный цикл Think → Plan → Build → Review → Test → Ship → Reflect; plan-review (челлендж постановки до работы, 2–3 вопроса в духе /office-hours); pre-ship check — обязательный шлюз перед «готово» (суть в первом предложении, ссылки на месте, проверено, нет утечек/дыр, сказано что изменилось); дизайн-задачи → gpt-image с идеей /design-shotgun (3–5 вариантов макета, выбор, вкус в карточку).
- Что НЕ переносится: личные slash-команды/скрипты gstack (заточены под Claude Code), iOS QA, дизайн-пайплайн с GPT Image для обложек (обложки — Pollinations), GStack Browser.
- Аналоги уже есть: grill-me ≈ office-hours, code-audit ≈ cso, postmortem ≈ investigate/retro, safe-release ≈ careful, agent-browser ≈ browse.
- CORE обновлён 08.08: обложки → только Pollinations; дизайн/UI-макеты и картинки под задачи (НЕ обложки) → gpt-image/iva-image, цену называть до запуска.
