---
type: note
description: >-
  upstage/solar-pro4 добавлена в TEXT_MODELS веб-панели (webapp/server.py) 11.08.2026: 524K контекст, цены 3.10/12.40 ₽ за 1М, efforts minimal…max.
tags: [webapp, models, routerai]
status: active
confidence: EXTRACTED
created: 2026-08-11
source: daily/2026-08-11.md
domain: knowledge
last_accessed: 2026-08-12
tier: active
relevance: 1.0
---

# Solar Pro 4 в веб-панели

Добавлена модель upstage/solar-pro4 (Solar Pro 4) в список TEXT_MODELS веб-панели `webapp/server.py` (после deepseek-v4-flash-0731).

Параметры: short «Solar Pro 4», in 3.10 / out 12.40 ₽ за 1М токенов, note «524K контекст · агентские задачи и код · уровни размышления», efforts = FULL_EFFORTS (minimal…max). Поддерживает reasoning, tools, structured_outputs (проверено через /api/v1/models).

Курс пересчёта цен: USD→RUB ≈ 0.962 (из deepseek-v4-flash-0731: 9.30 ₽ / 9.6649 $). Solar: $3.22/$12.89 → 3.10/12.40 ₽.

Веб-панель берёт модели из TEXT_MODELS на лету, статику править не нужно. Выбор модели пишет ROUTERAI_MODEL в .env и перезапускает iva.service. Webapp перезапущен (iva-webapp.service), синтаксис проверен.

## Related

- [[cards/projects/сайт-toharo-lab-github-pages-контент-платформа]]
