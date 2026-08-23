---
type: "project"
description: "Утверждён последовательный план оптимизации Iva: baseline/eval → runaway limits → background worker → batch tools → lazy skill references → memory worker → thin root/skill router. Этапы 1 и 2 завершены и приняты; этап 3 (узкий worker для фоновых задач) ждёт отдельного решения владельца."
tags: ["iva","token-optimization","evals","workflow"]
status: "active"
confidence: "EXTRACTED"
domain: "work"
created: "2026-08-23"
source: "daily/2026-08-23.md"
last_accessed: "2026-08-24"
tier: "active"
relevance: 1.0
---

# Оптимизация Iva: 7 этапов снижения токенов

**План:**
1. Baseline и eval.
2. Ограничение runaway-ходов.
3. Узкий worker для фоновых задач.
4. Batch tools вместо длинных bash/tool-цепочек.
5. Крупные skills → lazy references.
6. Memory worker.
7. Только затем облегчение root-инструкций и skill router.

**Этап 1 — 2026-08-23.** Созданы `data/custom/scripts/iva-eval-baseline.py` и `data/custom/evals/iva-optimization/` с PLAN, manifest, 8 фиксированными quality fixtures и версионированным run. Скрипт read-only, не вызывает LLM/API, исключает содержимое и session/turn IDs, считает usage и matched trace. Финальный baseline: 198 ходов, 2737 model calls, 216906161 input; ≥20 шагов — 43 хода и 64.53% input, ≥30 — 30 и 51.22%, ≥50 — 7 и 16.85%; trace coverage 145/198. Deterministic render, invariants, py_compile и selfcheck прошли; fresh adversarial review — ready/low risk.

**Этап 2 — 2026-08-23, завершён.** Пороги приняты владельцем: soft 20, diagnostic 30, hard cooperative cancel 50. Реализация — `data/custom/scripts/iva-watchdog.py` под отдельным systemd timer с периодом 30 секунд, рестарт Iva не требуется. Watchdog считает реальные usage rows, агрегирует в бюджет верхнего хода родителя, inline-субагентов и прямых дочерних субагентов по lineage, отменяет только доказанно активный ход через authenticated cancel route, трактует `accepted` как запрос и подтверждает отмену по исчезновению точного `workflowRun`, повторяет через 90 секунд. Eve run JSON и Telegram inbox не мутируются, журнал событий content-free и 0600.

Внешний агент нашёл и исправил один дефект: при неполном чтении каталога runs состояние отслеживаемого хода терялось, из-за чего повторно логировались пороги и обнулялась 90-секундная пауза. Теперь при недостоверном scan отмена откладывается, состояние удерживается с горизонтом шесть часов. Contract `PASS` по 13 критериям; тесты: py_compile, 13 core + 2 lineage + 5 scan-incomplete fixtures, systemd verify, selfcheck.

Жёсткая отмена доказана на disposable-сессии: `accepted` и терминальное `turn.cancelled`. На реальном Telegram-ходе 23.08 подтверждены детект и путь запроса: soft 21 → diagnostic 33 → hard 51 → cancel accepted. Что ход завершила именно отмена — не доказано: запись турна закрылась как `completed` через 4,5 секунды, а дочерние сессии позже погасил собственный механизм Eve `execution.terminate-child-sessions`. Практический вывод остаётся: общий бюджет верхнего хода расходуется заметно быстрее, когда ход оркестрирует субагентов — 18 собственных вызовов родителя против 51 в сумме с четырьмя детьми.

**Gate:** этап 3 начинается только по отдельному решению владельца. Перед проектированием снять 2–3 дня post-stage2 наблюдений и сравнить с baseline: число ходов ≥20/30/50, их доля input, число hard cancellation и false positive.

## Related

- [[cards/decisions/пилот-явного-prompt-caching-для-iva]]
- [[cards/notes/curator-hamel-husain]]
