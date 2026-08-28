---
type: "project"
description: "План из 7 этапов закрыт владельцем 24.08.2026 как неподходящий: выполнены только этапы 1–2, реальный эффект дал другой рычаг — окно контекста 272к→140к."
tags: ["iva","token-optimization","evals","workflow","closed"]
status: "cancelled"
confidence: "EXTRACTED"
domain: "work"
created: "2026-08-23"
source: "daily/2026-08-23.md"
last_accessed: "2026-08-24"
tier: "active"
relevance: 0.925
updated: "2026-08-24"
---
# Оптимизация Iva: 7 этапов снижения токенов

План закрыт владельцем 24.08.2026: после разбора внешним агентом признан неподходящим в исходном виде («логи посмотри, план запускался, потом почистили хвосты и провели другие варианты оптимизации»).

Выполнено из плана:
- Этап 1 (baseline): 198 ходов, 2737 model calls, 216,9 млн input; ходы ≥20 шагов = 43 шт и 64,53% input. Артефакты: `data/custom/scripts/iva-eval-baseline.py`, `data/custom/evals/iva-optimization/`.
- Этап 2 (watchdog runaway): пороги soft 20 / diagnostic 30 / hard cancel 50; `data/custom/scripts/iva-watchdog.py` принят, затем при чистке хвостов таймер отключён (iva-watchdog.timer disabled, можно включить одной командой).

Почему закрыт: внешний анализ (`data/custom/evals/iva-optimization/context-cost-report-20260823.md`) показал, что постоянный контекст ни при чём (~10k токенов минимума), реальный расход гонят долгоживущие сессии (75,1% чат-input в сессиях ≥10 ходов) и поздняя компактация (порог 190,4к при окне 272к). Облегчение root-инструкций (этап 7) дало бы единицы процентов.

Сделано вместо: `CODEX_CONTEXT_WINDOW` в `.env` 272000 → 140000, порог компактации 98 000; верхняя граница ожидаемой экономии ~20% чат-input. Замер эффекта рекомендован через 2–3 дня против baseline.

Отложенные рычаги (требуют правок апстримовского кода, отдельно не решено): ротация чат-сессий, ограничение размера результатов tools (наблюдались скачки до +139k за один шаг).

## Related

- [[cards/decisions/пилот-явного-prompt-caching-для-iva]]
- [[cards/notes/curator-hamel-husain]]

## History

- 2026-08-23: План: 1. Baseline и eval. 2. Ограничение runaway-ходов. 3. Узкий worker для фоновых задач. 4. Batch tools вместо длинных bash/tool-цепочек. 5. Крупные skills → lazy references. 6. Memory worker. 7. Только затем облегчение root-инструкций и skill router.

## Log

- 2026-08-24: Статус уточнён 24.08.2026: план закрыт, статус карточки — cancelled (в предыдущей записи статус остался active механически).
- 2026-08-24: 2026-08-23: В 20:30 владелец остановил разработку плана на этапе 2 (gate оставался FAIL, fresh-evaluator не пройден); для продолжения внешним агентом созданы data/custom/evals/iva-optimization/EXTERNAL-AGENT-HANDOFF.md и EXTERNAL-AGENT-PROMPT.md.
