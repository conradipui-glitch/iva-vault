---
type: "decision"
description: "21.08 по просьбе владельца изучен github.com/kunchenguid/grok-ship и адаптированы три механики в custom-слой: iva-factory (sqlite-бэклог scout/ship с промоушеном), adversarial-review, ahoy; все три протестированы на реальных задачах."
tags: ["grok-ship","iva-factory","workflow","review","custom-layer"]
status: "active"
confidence: "EXTRACTED"
domain: "work"
created: "2026-08-22"
source: "daily/2026-08-22.md"
last_accessed: "2026-08-22"
tier: "warm"
relevance: 0.865
---

# grok-ship: scout/ship + adversarial review + ahoy адаптированы для Ивы

21.08.2026 владелец попросил изучить github.com/kunchenguid/grok-ship («дистрибутив агента»: Scout vs Ship, локальный sqlite-бэклог, adversarial review, «мержишь только ты», firstmate/crewmates, lavish-axi, ahoy) и адаптировать полезное под нашу архитектуру в custom-слой, чтобы обновление не ломало. Взято три механики: 1) iva-factory — лёгкий sqlite-бэклог data/custom/factory.db с задачами scout (исследование/диагностика → отчёт, без изменений) и ship (авторизованное изменение), промоушен scout→ship флипает ту же задачу без дубликата; 2) adversarial-review — формализованный гейт перед «готово»: свежий субагент, verdict с severity (error/warning/info), action и risk_level; 3) ahoy — рекап сессии по запросу: сводка с последнего сообщения владельца + открытые решения. Не взято: crewmate/firstmate (мультибот чужой платформы), lavish-axi (долгий poll + браузер владельца, фоновые процессы у нас запрещены), sqlite как замена tasks/vault (взята только схема). Тест на близких задачах: scout — разбор 34 «НОВОЕ» selfcheck; ship + adversarial review — удаление устаревшей записи CLAUDE.md из tree-allowlist.json (verdict ready, risk low); ahoy — выдан рекап сессии.

## Related

- [[cards/decisions/gstack-workflow-адаптация-методологии-под-иву]]
- [[cards/notes/блокнот-сессии]]
