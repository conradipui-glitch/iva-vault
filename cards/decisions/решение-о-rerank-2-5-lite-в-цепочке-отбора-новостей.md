---
type: decision
description: >-
  06.08.2026 решено добавить rerank-2.5-lite как «спасателя» в цепочку отбора новостей (после embedding-дедупликации, перед LLM-оценкой); эмбеддинги bge-m3 + косинус
tags: [news, rerank, bge-m3, pipeline, decision]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-07
source: daily/2026-08-07.md
access_count: 1
last_accessed: 2026-06-28
relevance: 0.295
tier: cold
---

# Решение о rerank-2.5-lite в цепочке отбора новостей

06.08.2026 решено: добавить rerank-2.5-lite на позицию «спасателя» в цепочку отбора новостей (после embedding-дедупликации, перед LLM-оценкой). Эмбеддинги: bge-m3 + косинус. Предложен тест на 20 кандидатах для проверки эффекта. Цель — не пропускать релевантные новости, которые теряются на embedding-этапе.

## Related
- [[cards/projects/тренд-монитор-hn-github-arxiv-скрипт-компаньон]]
