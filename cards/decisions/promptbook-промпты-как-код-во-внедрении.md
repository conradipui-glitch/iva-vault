---
type: "decision"
description: "По команде владельца «тяни код из репозитория и внедряй согласно правилам» (23.08) Promptbook добавлен вендор-копией в custom-слой: CLI iva-promptbook.py и книга promptbook-integration.json; ревью шли до готовности, апстрим Ивы не затронут."
tags: ["promptbook","prompts-as-code","workflow","custom-layer","vendor"]
status: "active"
confidence: "EXTRACTED"
created: "2026-08-24"
source: "daily/2026-08-23.md"
domain: "work"
last_accessed: "2026-08-25"
tier: "active"
relevance: 0.895
---

# Promptbook: промпты как код во внедрении

23.08 владелец спросил про pbook.dev (open-source управление системными промптами как кодом: фрагменты в Markdown, условия и варианты в YAML), затем вел: тянуть код из репозитория, чтобы не переизобретать части, внедрять полностью или частично и строго согласно правилам custom-слоя, чтобы обновление Ивы ничего не ломало.

Реализация (всё в custom-слое, апстрим Ивы не тронут):
- вендор-копия репозитория: data/custom/vendor/promptbook;
- CLI: data/custom/scripts/iva-promptbook.py и test_iva_promptbook.py;
- интеграционная книга: data/custom/promptbooks/promptbook-integration.json.

Adversarial review шёл несколькими раундами: fixes_needed по пину (pinned commit не закреплял runtime-артефакт и дерево зависимостей; resolve исполнял dist из ignored-путей), отсутствию forbid-правила в post.yaml, слабому smoke (не покрывал path containment, размер, UTF-8, pin mismatch). Финальный вердикт NEEDS_WORK: критерий 6 не доказан артефактами — нет записанного прогона upstream core typecheck, content-learning check и iva-selfcheck --skills; кастомный тест проверял только собственные smoke-утверждения. Базовая сборка промптов работает; полное закрытие проверками в транскрипте дня не зафиксировано.

## Related

- [[cards/decisions/gstack-workflow-адаптация-методологии-под-иву]]
- [[cards/projects/оптимизация-ива-7-этапов-снижения-токенов]]
- [[cards/ideas/самообучающаяся-контент-система]]
