---
type: note
description: >-
  Upstage Solar Pro 4 добавлена в TEXT_MODELS веб-панели (webapp/server.py), цены 3.10/12.40 ₽ за 1М, полный набор efforts, контекст 524K.
tags: [iva-webapp, routerai, models]
status: active
confidence: EXTRACTED
domain: ops
created: 2026-08-11
source: daily/2026-08-11.md
last_accessed: 2026-08-12
tier: "cold"
relevance: 0.58
---

# Добавление модели Solar Pro 4 в веб-панель

11.08.2026: в `webapp/server.py` в `TEXT_MODELS` добавлена `upstage/solar-pro4` (Solar Pro 4) после deepseek-v4-flash-0731: `{"id": "upstage/solar-pro4", "short": "Solar Pro 4", "in": 3.10, "out": 12.40, "note": "524K контекст · агентские задачи и код · уровни размышления", "efforts": FULL_EFFORTS}`.

Цены: API routerai $3.22/$12.89 за 1М токенов → ≈ 3.10/12.40 ₽ (курс из сопоставления с qwen3.7-flash и deepseek-v4-flash-0731). Модель поддерживает reasoning (уровни минимальный..max), tools, structured_outputs. Контекст 524K (в панели окно ограничено 32–100K — окно выбирается отдельно, не из модели).

Панель (webapp/static/index.html) рендерит модели из `TEXT_MODELS` — отдельный список не нужен. При выборе в панели пишется `ROUTERAI_MODEL` в `.env` и перезапускается iva.service. webapp перезапущен (21:54), активен.

Урок: eve при рестарте посреди активного рана переисполняет inline-шаги — запись файла из одного шага выполнилась 3 раза (пришлось дедуплицировать регуляркой).
