---
type: decision
description: >-
  Внедрение трёх harness-примитивов (Default-FAIL, свежий оценщик, handoff) в воркфлоу Ивы по статье Sprytixl/Anthropic; скилл harness-primitives.
tags: [harness, agents, workflow, quality, anthropic]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-12
source: daily/2026-08-12.md
last_accessed: 2026-08-14
tier: active
relevance: 1.0
---

# Внедрение harness-примитивов

Владелец прислал X-статью Sprytixl про харнесс для длинных агентных задач (Anthropic, 400k сессий Claude Code, 235k разработчиков; METR: 50% task horizon удваивается ~каждые 7 месяцев; Default-FAIL, свежий оценщик, handoff; Kimi Code/K3 как open-source путь).

12.08.2026 по решению владельца («Внедри примитивы», msg 1612) создан custom-скилл `data/custom/agent/skills/harness-primitives/`:
- Default-FAIL: критерии приёмки в контракт-файле test-results.json (шаблон), «готово» = доказанный факт;
- Свежий оценщик: отдельный агент без истории, вердикт PASS / NEEDS_WORK (шаблон evaluator.md);
- Handoff-файл: PROGRESS.md (шаблон) для многосессионных задач; handoff + git = внешняя память.

Применять для крупных/долгих задач; для простых — не нужно (урок Agentless: сложность должна соответствовать задаче).

Связанные репозитории: github.com/anthropics/cwc-long-running-agents (641⭐, Apache-2.0, демо-набор примитивов), github.com/MoonshotAI/kimi-code (6.4k⭐, CLI-агент, субагенты plan/explore/coder), github.com/MoonshotAI/Kimi-K3 (8.4k⭐, модель 2.8T MoE, 1M контекст; локально нужен кластер H100/H20 — только API).

## Related

- [[cards/notes/harness-primitives-внедрение]]
