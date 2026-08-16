---
type: decision
description: >-
  Жёсткий лимит Threads — 500 знаков на пост. Все тексты для Threads проверять len(text)<=500 до постановки в очередь (iva-queue/iva-threads-api-post). Причина: 16.08.2026 задача упала с 684 знаками.
tags: [threads, publishing, limit, rule, content]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-16
source: daily/2026-08-16.md
last_accessed: 2026-08-17
tier: active
relevance: 1.0
---

# Правило: Threads-тексты строго ≤500 знаков, проверять до постановки в очередь

16.08.2026 после падения задачи threads-vision (текст 684 знаков, лимит Threads 500) зафиксировано правило:

- Любой текст для публикации в Threads (через iva-threads-api-post / iva-queue) проверять длину ДО постановки в очередь: len(text) <= 500.
- При генерации через iva-write (модель opus46) сразу указывать лимит «≤500 знаков» и проверять результат.
- Компактный формат: ~450-500 знаков, включая строку «Источник: …». Сокращать до ~450-480 для запаса.
- После сокращения пересоздавать задачу в очереди (cancel + add), старые длинные тексты не оставлять.

Причина: Threads API жёстко режет — MAX_LEN=500 в iva-threads-api-post.py, ошибка «текст N знаков, лимит Threads 500» роняет задачу, пост не выходит.

## Related

- [[cards/projects/threads-личный-аккаунт-про-ии-без-котиков]]
- [[cards/projects/iva-write-пул-исполнителей-подписки]]
