---
type: note
description: >-
  Минимальное наблюдение за VPS: логи, функциональные проверки, алерты и границы мониторинга.
tags: [curator, infrastructure, monitoring, logs, uptime-kuma, alerts, observability]
status: active
confidence: INFERRED
domain: knowledge
created: 2026-08-01
source: christian-lempa-corpus-curated
last_accessed: 2026-08-04
tier: active
relevance: 1.0
---

# Наблюдаемость без монолитов

Начинай с простых проверок, которые отвечают на реальный вопрос: работает ли нужная функция.

- Для Docker: состояние, `docker stats`, короткий хвост логов и функциональный запрос.
- Для IVA: systemd status, journal и тест Telegram-сценария.
- Для внешних сервисов: HTTP/TCP проверка плюс уведомление при падении и восстановлении.
- Uptime Kuma подходит для лёгкого контроля доступности; не запускай тяжёлый стек логирования на 4 GB RAM без причины.
- Мониторинг не должен сам создавать нагрузку: не вызывай LLM и тяжёлый workflow каждую минуту ради health-check.

Алерт полезен, только если у него есть владелец, понятный порог и действие после получения.
