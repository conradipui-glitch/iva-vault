---
type: note
description: >-
  Опыт публикации первого интерактивного поста на toharo-lab: деплой падает при обложке не-16:9, интерактивные MDX-компоненты регистрируются в mdx-components.tsx, человекизация текста убирает ИИ-паттерны
tags: [toharo-lab, обложки, деплой, mdx]
status: active
confidence: EXTRACTED
created: 2026-08-11
source: daily/2026-08-11.md
domain: knowledge
last_accessed: 2026-08-11
tier: active
relevance: 0.91
---

# toharo-lab: деплой и обложки (интерактив, 16:9, Actions)

## Публикация интерактивного поста «Шесть моделей, одна задача, ноль иллюзий» (11.08.2026)

- Пост с интерактивом: `content/posts/shest-modeley-odna-zadacha.mdx`, компоненты `src/components/pool-interactive.tsx` (PoolChart + ModelVersions), зарегистрированы в `src/components/mdx-components.tsx`. Клик по модели показывает её данные и полный текст.
- **Деплой падает при обложке не-16:9**: check-posts.mjs требует 16:9 (1.78:1). Обложка GPT Image 2 по умолчанию 1536×1024 (1.5:1) → деплой failed. Фикс: обрезка через PIL до 1536×864. Все обложки теперь 16:9.
- Перегенерация обложки tri-sloya: была абстрактная (нерелевантна), теперь три горизонтальных слоя: листы правил / дерево решений / шестерни кода. Стиль: кремовый фон #fffdf7, лаймовый акцент #c9ff3d, тёмные линии #14140f.
- **Человекизация**: владелец просит убирать ИИ-паттерны («Первое/Второе», «есть X, есть Y», «не X, а Y», «самый X, самый Y», повторы, канцелярит). Готового скилла humanizer нет; правка вручную по смыслу, все цифры сохранять.
- Живой сайт: https://conradipui-glitch.github.io/toharo-lab/blog/shest-modeley-odna-zadacha/ (HTTP 200).
- Коммиты: f1f87bc (пост+интерактив), 537ff89 (обложки).

## Related
- [[cards/notes/toharo-lab-обложки-gpt-image-2-через-routerai]]
