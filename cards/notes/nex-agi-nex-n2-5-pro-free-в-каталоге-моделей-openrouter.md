---
type: "note"
description: "09.09.2026: в список выбора моделей Ивы добавлена nex-agi/nex-n2.5-pro:free (OpenRouter, бесплатная, 262K ctx, проверена живым запросом)"
tags: ["models","openrouter","iva","catalog"]
status: "active"
confidence: "EXTRACTED"
created: "2026-09-10"
source: "daily/2026-09-10.md"
domain: "knowledge"
last_accessed: "2026-09-10"
tier: "active"
relevance: 0.985
---

# nex-agi/nex-n2.5-pro:free в каталоге моделей OpenRouter

09.09.2026: по просьбе Антона в каталог моделей OpenRouter добавлена nex-agi/nex-n2.5-pro:free — бесплатная, контекст 262K, проверена живым запросом (отвечает, tool calling работает, reasoning_effort принимает). Добавлена в `scripts/lib/model-catalog.ts` → доступна в `/model` при выборе провайдера OpenRouter; пересобрано через eve build. Текущая модель Ивы при этом не менялась (провайдер B.AI); для переключения нужен `MODEL_PROVIDER=openrouter` + `OPENROUTER_MODEL=nex-agi/nex-n2.5-pro:free` в `.env` и `iva restart` владельцем. У free-модели у OpenRouter есть лимиты запросов/скорости.

## Related

- [[cards/notes/провайдер-b-ai-ива]]
- [[cards/notes/deepseek-v4-flash-vision-exp-подключена-как-vision-модель-ивы]]
- [[cards/notes/solar-pro-4-в-веб-панели]]
