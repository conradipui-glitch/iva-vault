---
type: decision
description: >-
  Аккаунт X @TrampampamAGI забанен за inauthentic behaviors 06.08.2026; владелец подал апелляцию; постинг вручную; куки X не использовать
tags: [x, suspension, account, social]
status: active
confidence: EXTRACTED
domain: social
created: 2026-08-06
source: daily/2026-08-06.md
last_accessed: 2026-08-07
tier: "cold"
relevance: 0.52
---

# X-аккаунт TrampampamAGI заблокирован (апелляция подана)

# X: блокировка и решение

## Факты (06.08.2026)
- X-аккаунт @TrampampamAGI (id 2053711559893905408, name «A Cat Boris») заблокирован за нарушение правил — «inauthentic behaviors» (неподлинное поведение). Письмо от X Support 06.08.2026.
- API-доступ с кук x.env уже был заблокирован ранее (403 code 64 suspended, upload_media). Чтение (fetch_me) работало.
- Владелец заметил: в постах X вместо изображений — пустой квадрат.
- Апелляция подана владельцем вручную через форму X (06.08.2026). Решение по официальному API — в процессе.

## Решение владельца (06.08.2026)
- **X: постим вручную с телефона**, пока не решится вопрос с официальным постингом через API.
- **Посты в X в будущем — без изображений** (показываются пустым квадратом).
- **Threads: только через официальный API** (iva-threads-api-post).
- **Куки threads.env и x.env — в резерве; запросов оттуда быть не должно нигде, включая n8n.**

## Технические действия (выполнено)
- В /etc/crontab закомментированы: x-auto-post (04/09/15), x-weekly-report (вс), threads-monitor (5-19ч).
- systemd-юнит iva-x-reader-gateway.service отключён (disable --now).
- health-watch.sh: блок проверки cookie X вырезан (NEED_COOKIE=0).
- n8n: активных воркфлоу с X/Threads нет; креды X/Threads отсутствуют.
- ai-social-monitor (docker): не запущен, токены пусты.

## Статус
- Апелляция: подана, ждём. Если отказ — повтор каждые 48ч (часто проходит с 3-й попытки).
- До разблокировки: НЕ создавать новый аккаунт с того же IP, не дёргать старый.
- При разблокировке: вернуть cron-записи X из бэкапа /etc/crontab.bak-20260806-xfreeze.

## Related
- [[cards/contacts/антон-владелец.md]]
