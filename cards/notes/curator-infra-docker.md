---
type: note
description: Практика Docker Compose для stateful и stateless сервисов на одиночном VPS.
tags: [curator, infrastructure, docker, compose, postgres, volumes, versions]
status: active
confidence: INFERRED
domain: knowledge
created: 2026-08-01
source: christian-lempa-corpus-curated
last_accessed: 2026-08-04
tier: warm
relevance: 0.76
---

# Docker Compose без лишней сложности

Compose-файл — воспроизводимое описание сервиса, а не одноразовая шпаргалка.

- Используй конкретные версии образов; обновляй после чтения changelog и создания бэкапа.
- Для данных одиночного VPS допустимы локальные named volumes или bind mounts, если бэкап уходит за пределы VPS.
- PostgreSQL и прочие stateful-сервисы не выставляй в интернет через `ports` без необходимости.
- Разделяй публичную и внутреннюю Docker-сети, когда это действительно снижает риск.
- Перед запуском проверяй `docker compose config`.
- После запуска проверяй состояние, последние логи и реальную функцию, а не только наличие контейнера.

`latest` не используй как рабочую стратегию обновления. Автоматизация обновлений допустима только с уведомлением, контролем изменений и откатом.
