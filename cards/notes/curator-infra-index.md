---
type: note
description: >-
  Маршрутизатор библиотеки инфраструктурных принципов: когда и какие карточки использовать для VPS, Docker, n8n и IVA.
tags: [curator, infrastructure, vps, docker, n8n, iva, christian-lempa]
status: active
confidence: INFERRED
domain: knowledge
created: 2026-08-01
source: christian-lempa-corpus-curated
last_accessed: 2026-08-04
tier: warm
relevance: 0.745
---

# Инфраструктурный куратор: индекс

Это библиотека рабочих принципов, извлечённых из публичного корпуса Christian Lempa и адаптированных под текущий одиночный VPS. Это не имитация человека и не обязательная инструкция на каждый ход.

## Как выбирать карточки

- Новый сервис или деплой: `curator-infra-deploy` + `curator-infra-docker`.
- Падение, ошибка, недоступность: `curator-infra-diagnosis`.
- RAM, swap, OOM, медленный сервер: `curator-infra-resources`.
- n8n или workflow: `curator-infra-n8n`.
- IVA или Telegram-мост: `curator-infra-iva-systemd`.
- Обновление: `curator-infra-updates` + `curator-infra-backup-rollback`.
- Бэкап, восстановление, опасное изменение: `curator-infra-backup-rollback`.
- SSH, порты, reverse proxy, TLS: `curator-infra-network`.
- Мониторинг и алерты: `curator-infra-observability`.

## Лимит контекста

До действия находи через `memory_search` и читай максимум 1–3 релевантные карточки. Не загружай весь набор и не используй карточку как замену фактической проверки хоста.
