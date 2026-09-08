---
type: note
description: >-
  Прогон nuwa-фабрики по 3 тарифам (Быстрый/Стандарт/Глубокий) на примере Simon Willison: замер токенов, quality check 6/6, рекомендация по выбору тарифа.
tags: [nuwa, skills, tokens, test-run, content-pipeline]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-10
tier: "cold"
relevance: 0.565
source: daily/2026-08-10.md
last_accessed: 2026-08-11
---

# nuwa-тестовый-прогон-3-тарифа-willison

## Тестовый прогон nuwa: Simon Willison → скилл «куратор-редактор AI-новостей» (10.08.2026)

Задача 8 закрыта. Прогон по всем 3 тарифам через codex (gpt-5.6-terra), пример — Willison (куратор новостей ИИ).

### Замер токенов (полный синтез research → SKILL.md, codex exec --json)
| Тариф | input | cached | output | reasoning | Σ |
|---|---|---|---|---|---|
| Быстрый | 17 380 | 13 056 | 2 104 | 52 | 19 536 |
| Стандарт | 19 294 | 11 008 | 3 105 | 46 | 22 445 |
| Глубокий | 19 706 | 11 008 | 3 584 | 53 | 23 343 |

### Quality check: все 6/6 PASS
- Ментальные модели: 5/6/6; Ограничения ✅; DNA 7 маркеров; Честные границы 5/6/6; Напряжения 5/7/7; Первоисточники 83/75/77%.

### Выводы
- Разница токенов между тарифами скромная (+15% Быстрый→Глубокий), но качество растёт (глубже модели, напряжения, крупнее SKILL.md).
- Рекомендация: Стандарт — золотая середина для реальной дистилляции; Быстрый — для черновиков/массовых персон; Глубокий — для ключевых персон.
- Кэш работает: cached ≈ 60–75% от input.

### Технические заметки
- codex вне git-репо требует `--skip-git-repo-check`.
- usage отдаётся в событии `turn.completed` (input/cached/output/reasoning).
- quality_check.py требует секции: 心智模型 (3-7 шт), 局限, 表达DNA (≥3 маркера), 诚实边界 (≥3 пункта), 张力 (≥2), 来源 с 一手>50%.
- Артефакты: /tmp/nuwa-test/{fast,standard,deep}/SKILL.md (+research_full.md, usage.json), run_tier.sh.

### Статус
Скиллы НЕ установлены в data/custom — ждут решения владельца (пересборка + рестарт нужны). Субагентские версии SKILL_subagent.md сохранены для сравнения.

## Related
- [[cards/notes/nuwa-skill-фабрика-персональных-скиллов-distill-person-skill]]
- [[cards/notes/куратор-threads-формула-постинга-и-x-алгоритм]]
