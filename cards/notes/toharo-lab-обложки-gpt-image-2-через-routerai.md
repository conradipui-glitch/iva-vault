---
type: note
description: >-
  Перегенерация 3 обложек сайта toharo-lab через openai/gpt-image-2 (routerai) — контракт, размеры, сжатие, деплой.
tags: [toharo-lab, gpt-image-2, routerai, covers]
status: active
confidence: EXTRACTED
created: 2026-08-11
source: daily/2026-08-11.md
domain: knowledge
last_accessed: 2026-08-11
tier: "warm"
relevance: 0.82
---

# toharo-lab обложки: GPT Image 2 через routerai

## Что сделано (11.08.2026)

Сайт toharo-lab (repo conradipui-glitch/toharo-lab, публичный, статический Next.js → Pages). Три обложки перегенерированы через **openai/gpt-image-2** на routerai, единый стиль (кремовый фон, лаймовый акцент, плоская векторная графика, без текста).

- Слаги: `agents-md-pravila-dlya-agentov`, `skills-claude-code-svoi-navyk`, `tri-sloya-nadezhnogo-agenta`.
- `.env.local` в корне репо (в .gitignore, НЕ коммитится): `OPENAI_API_KEY=ROUTERAI_API_KEY`, `OPENAI_BASE_URL=https://routerai.ru/api/v1`, `OPENAI_IMAGE_MODEL=openai/gpt-image-2`.
- `npm run cover -- --slug <slug> --provider openai --force --prompt "..." --alt "..."` — рабочий контур.

## Контракт routerai для gpt-image-2 (проверено живыми запросами 11.08)

- `POST https://routerai.ru/api/v1/images/generations`, Bearer ROUTERAI_API_KEY.
- Поддерживает `aspect_ratio` (1:1, 3:2, 4:3, 16:9, 21:9, 9:16, 2:3, 3:4, auto), `quality` (auto/low/medium/high), `background` (auto/opaque), `n`, `input_references`, `output_compression`. `size` НЕ в списке supported_parameters, но **принимается без ошибки** и даёт картинку 1536x1024 (как и aspect_ratio=16:9).
- Ответ: `data[0].b64_json` (base64 PNG) — make-cover.mjs его понимает.
- Цена: 0.61 ₽/картинка (записано в IMAGE_PRICES mediagen.py).

## Сжатие (важно для будущих обложек)

- GPT Image 2 отдаёт PNG 1536x1024, скрипт пишет его как `.jpg` → файл ~1.5–1.8 МБ.
- Плоская векторная графика отлично жмётся в настоящий JPEG (Pillow, quality=85, optimize, progressive): 1647→52, 1778→58, 1519→79 КБ. Визуально идентично. Делать всегда.

## Деплой

- `npm run check` (check-posts + check-secrets) и `npm run build` зелёные.
- Коммит `covers: перегенерация обложек через GPT Image 2`, push → Actions Deploy to GitHub Pages (1м9с, success).
- Живой сайт: https://conradipui-glitch.github.io/toharo-lab/ — все три обложки отдаются 200.
- Ключ в истории не попадал (git log -p -S не находит).

## Контекст

- AGENTS.md: репо публичный, никаких секретов (pre-commit хук check-secrets), статическая сборка, slug = URL неизменен, проверки перед пушем, без серверного кода.
- Владелец репо — conradipui-glitch (gh авторизован, https).

## Related
- [[cards/projects/iva-write-пул-исполнителей-подписки]]
- [[cards/notes/озвучка-youtube-конвейер-iva-yt]]
