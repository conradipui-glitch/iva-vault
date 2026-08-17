---
type: note
description: >-
  Перегон 12 кураторских персон vault → nuwa-скиллы через codex (10.08.2026): 13 скиллов 6/6, ~233К токенов.
tags: [nuwa, skills, codex, content-pipeline, batch]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-10
tier: active
relevance: 0.895
source: daily/2026-08-10.md
last_accessed: 2026-08-11
---

# перегон-персон-nuwa-12-скиллов

## Перегон 12 кураторских персон → nuwa-скиллы (10.08.2026)

Задача 11 закрыта. Все 13 скиллов-перспектив готовы, все 6/6 quality_check с первой попытки.

### Созданные скиллы (data/custom/agent/skills/)
ai-security-perspective, andrej-karpathy-perspective, april-dunford-perspective, chris-do-perspective, ethan-mollick-perspective, hamel-husain-perspective, jerry-liu-perspective, maxim-ilyakhov-perspective, misha-tokovinin-perspective, patrick-boyle-perspective, simon-willison-news-curator-perspective, steve-schoger-perspective, vibe-product-perspective.

Каждый: SKILL.md + references/research/ + usage.json + quality.txt.

### Тарифы и токены
- Глубокий (karpathy 40К, ai-security 18К) — реально дороже из-за полной загрузки первоисточников.
- Стандарт (~17.5К): mollick, husain, liu, dunford, ilyakhov, boyle, schoger, willison.
- Быстрый (~17.3К): chris-do, tokovinin, vibe-product.
- Σ ≈ 233 000 токенов на весь перегон. Все прошли с 1-й попытки (карточки vault — хорошая база).

### Технические заметки
- run_batch.sh: `while read` в пайпе не работает (подшелл) — запускать цикл напрямую.
- codex требует `--skip-git-repo-check` вне git-репо.
- Скиллы подхватятся после пересборки + рестарт (делает владелец).

### Связи
- Карточки-источники: vault/cards/notes/curator-*.md
- Решение: cards/decisions/контент-через-кодекс-и-перегон-персон-nuwa.md

## Related
- [[cards/decisions/контент-через-кодекс-и-перегон-персон-nuwa]]
- [[cards/notes/nuwa-тестовый-прогон-3-тарифа-willison]]
