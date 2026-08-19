---
type: project
description: >-
  Пул моделей по подпискам (iva-write.py) с приоритетом доступности. 13.08: модель каждого поста логируется в data/posts.jsonl + write-pool-usage.jsonl; iva-post-provenance.py дописывает platform/url/model/perspectives/cost. 14.08: Antigravity CLI (Gemini 3.7 Flash) использован как исполнитель для статьи разоблачения.
tags: [codex, antigravity, content-pipeline, iva-write, pool, models, subscriptions, pipeline, provenance]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-11
source: daily/2026-08-11.md
last_accessed: 2026-08-11
tier: "warm"
relevance: 0.865
updated: 2026-08-15
---

# iva-write-пул-исполнителей-подписки

Собран пул исполнителей iva-write (11.08.2026) — единая обёртка для написания текстов через подписки.

## Суть
Обёртка `scripts/iva-write.py` (линк /usr/local/bin/iva-write): пробует модели по цепочке, возвращает первый прошедший проверку. Пул: opus46 (claude-opus-4-6-thinking, agy) → sonnet46 (claude-sonnet-4-6, agy) → terra (gpt-5.6-terra max, codex) → luna (gpt-5.6-luna medium, codex) → gemini36 (gemini-3.6-flash-medium, agy) → routerai (claude-sonnet-5, ПЛАТНЫЙ резерв).

## Результаты теста (11.08, материал «7 ИИ-поисковиков»)
- Победитель: opus46 — лучший хук («ни один домен не совпал у всех семерых. Вообще ни один»), точность, 899–1011 знаков, ~15с, бесплатно.
- sonnet46 — крепкий запасной, чуть длиннее.
- terra (max) — самый плотный (746–860 зн.), суховат; luna — детальный, с водой.
- gemini36 — клише и эмодзи; routerai — платно (2.67₽), без изюминки.
- Лимитов ни в одном контуре не упёрлись. Три независимых контура: routerai API, ChatGPT-подписка (codex), Google-подписка (agy).

## Технические заметки
- codex вне git-репо: --skip-git-repo-check. Версия клиента гейтит модели (CLIENT_VERSION в codex-oauth.ts, сейчас 0.144.0, установлен 0.146.0).
- Доступные модели codex через подписку: gpt-5.6-terra (efforts low..max), gpt-5.6-luna, gpt-5.5, gpt-5.4-mini.
- agy 1.1.10: модели gemini-3.6-flash (high/medium/low), gemini-3.1-pro, claude-opus-4-6-thinking, claude-sonnet-4-6.
- Gemini CLI на сервере мёртв (IneligibleTierError) — перешли на antigravity.
- cc-switch: GUI для десктопа, на сервере не нужен (всё залогинено напрямую). PR #5975 с antigravity-поддержкой не влит.
- Расход: data/write-pool-usage.jsonl; журнал старый data/agy-usage.jsonl.

## Решение владельца
Писать посты через пул подписок (бесплатно), routerai — только резерв. Claude-подписка владельца — только для его локальных проектов, в пул не включать.

## Related

- [[cards/decisions/контент-через-кодекс-и-перегон-персон-nuwa]]
- [[cards/notes/провенанс-постов-модель-специалисты-стоимость-iva-post-provenance]]

## Log

- 2026-08-14: 13.08.2026 (разбор в ходе дня): схема постинга — 1 модель по подписке, при недоступности следующая по приоритету (3-я и т.д.). Журналы: `write-pool-usage.jsonl` (пул), `data/posts.jsonl` с полем `model` (заполнялось редко, перспективы не писались). Добавлен `scripts/iva-post-provenance.py`: после каждой публикации дописывает запись (platform, url, model, perspectives, writer, cost); записаны 4 поста от 12.08.
- 2026-08-15: 14.08.2026: Antigravity CLI (Gemini 3.7 Flash) использован как исполнитель — через него переписана статья-разоблачение Claude AI Ultimate на сайт (deploy success). Подтверждено: пул исполнителей включает не только iva-write.py, но и Antigravity CLI как рабочий инструмент.
