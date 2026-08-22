---
type: "note"
description: "21.08 DeepSeek выпустила экспериментальную мультимодалку deepseek-v4-flash-vision-exp; Ива работает на DeepSeek API (deepseek-v4-flash) и подключила зрение отдельной переменной DEEPSEEK_VISION_MODEL в .env."
tags: ["deepseek","vision","model","env","config"]
status: "active"
confidence: "EXTRACTED"
domain: "work"
created: "2026-08-22"
source: "daily/2026-08-22.md"
last_accessed: "2026-08-22"
tier: "active"
relevance: 0.985
---

# deepseek-v4-flash-vision-exp подключена как vision-модель Ивы

Ива работает на DeepSeek API: текстовая модель deepseek-v4-flash (зрения у неё нет — картинки не распознавались). 21.08.2026 DeepSeek выпустила экспериментальную мультимодалку deepseek-v4-flash-vision-exp (зрение + текст, по агентским бенчам со зрением близка к Opus-4.8, официальный changelog от 21.08). Механизм отдельной vision-модели в коде уже был: в .env добавлена строка DEEPSEEK_VISION_MODEL=deepseek-v4-flash-vision-exp (бэкап .env.bak-ds-vision), текстовая модель не тронута. Применяется после рестарта (модель читается один раз при старте), откат — удалить строку. Вечером того же дня картинка уже распозналась (мем про тигровый рулет).

## Related

- [[cards/notes/solar-pro-4-в-веб-панели]]
- [[cards/notes/добавление-модели-solar-pro-4-в-веб-панель]]
