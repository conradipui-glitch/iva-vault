---
type: decision
description: >-
  Решение владельца (10.08.2026): все посты/задачи писать через codex для экономии токенов (тариф по ситуации), перегнать все персоны vault через nuwa в скиллы, при лимитах codex — делать самой.
tags: [codex, tokens, nuwa, content-pipeline, decision]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-10
tier: "cold"
relevance: 0.565
source: daily/2026-08-10.md
last_accessed: 2026-08-11
---

# контент-через-кодекс-и-перегон-персон-nuwa

## Решение (10.08.2026): контент через codex + перегон персон nuwa

Владелец утвердил (голосовое 23:19):
1. **Все посты и задачи для всего контента писать через codex** — для экономии токенов. Тариф по ситуации: Быстрый/Стандарт/Глубокий (глубокий — для конкретных вещей). Если codex упирается в лимиты — делать самой (обычным путём).
2. **Перегнать все персоны через nuwa**: все-все-все переделать/переформатировать в скиллы-перспективы.
3. Установлен скилл Simon Willison (Стандартный тариф): `data/custom/agent/skills/simon-willison-news-curator-perspective/` (6/6 quality_check, references/research/01-corpus.md). Требует пересборки + рестарт для подхвата.

## Список персон для перегона (13)
karpathy, ai-security, april-dunford, chris-do, ethan-mollick, hamel-husain, jerry-liu, maxim-ilyakhov, misha-tokovinin, patrick-boyle, simon-willison (готов), steve-schoger, vibe-product.

## Тарифы nuwa (из SKILL.md)
- Быстрый: 3 измерения, ≤5 источников — малоизвестная персона/экономия (~1/3 стоимости).
- Стандарт (дефолт): 6 измерений — большинство случаев.
- Глубокий: 6 измерений + полная загрузка первоисточников — на вырост/публикация.

## Технические ограничения
- codex вне git-репо: нужен `--skip-git-repo-check`.
- usage токенов в событии `turn.completed` (input/cached/output/reasoning).
- Замеры тарифов (Willison): Быстрый 19.5К, Стандарт 22.4К, Глубокий 23.3К токенов.
