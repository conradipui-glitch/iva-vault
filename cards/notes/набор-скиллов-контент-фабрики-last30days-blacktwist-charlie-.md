---
tier: active
relevance: 0.94
type: note
description: >-
  Сборка набора контент-скиллов (10.08.2026): last30days + 7 blacktwist + 6 charlie947 + x-algo-skill = 16 шт. без ключей, скопированы в data/custom/agent/skills/, ждут пересборки+рестарт.
tags: [skills, content-pipeline, last30days, x-algorithm, workflow]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-10
source: daily/2026-08-10.md
last_accessed: 2026-08-11
---

# набор-скиллов-контент-фабрики-last30days-blacktwist-charlie-xalgo

## Сборка набора скиллов (10.08.2026)

Анализ 8 репозиториев social-media-скиллов → собран набор 16 скиллов, скопированы в `data/custom/agent/skills/` (14 + x-algo = 15-й, итого 16 с nuwa-скиллом отдельно).

### Взято (без ключей, работают)
- **last30days** — исследовательский движок (Reddit/YouTube/HN/GitHub/Polymarket), протестирован, без API-ключей.
- **7 от blacktwist** (post-writer, thread-writer, hook-writer, content-repurposer, platform-strategy, social-media-context, content-pattern-analyzer).
- **6 от charlie947** (hook-generator, post-formatter, content-matrix, niche-research, post-writer-sms и др.).
- **x-algo-skill (attainmentlabs)** — реальная формула X-алгоритма (Phoenix от xai-org, январь 2026): 19 сигналов вовлечения (reply 30% / repost 25% / dwell 20% / like 15% / негатив −10%), 30-минутное правило, анти-паттерны. Ложится на Threads-конвейер (те же сигналы).

### Не взято
- **ScrapeCreators (13 скиллов)** — все требуют платный `SCRAPECREATORS_API_KEY` (бесплатно 10К кредитов при регистрации); без ключа мёртвые. Репозиторий склонирован в `data/tools/scrapecreators` на случай решения владельца.
- **x-use (MCP, браузерная автоматизация X)** — риск бана не снимается (undetected детектится X, аккаунт уже на апелляции) → вердикт «не внедряем» подтверждён (см. [[cards/notes/x-use-репозиторий-браузерная-автоматизация-x-не-для-нас]]).
- **langchain-ai/social-media-agent** — полный LangGraph-агент URL→пост, но Threads нет, тяжёлый стек, X вручную; забраны идеи reflection/evals (см. [[cards/notes/langchain-social-media-agent-полный-агент-не-для-нас-но-идеи]]).

### Статус
Сборка успешна (16 шт.), активация — после `npm run build` + `iva restart` (делает владелец). Вопрос владельцу: ядро (5) / средний (9) / все 14+ — решён: берём всё безключевое, ScrapeCreators — по запросу.

## Related
- [[cards/notes/куратор-threads-формула-постинга-и-x-алгоритм]]
- [[cards/notes/x-use-репозиторий-браузерная-автоматизация-x-не-для-нас]]
- [[cards/decisions/контент-через-кодекс-и-перегон-персон-nuwa]]
