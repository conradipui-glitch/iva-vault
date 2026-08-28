---
type: note
description: >-
  Оценка langchain-ai/social-media-agent: полный LangGraph-агент URL→пост (Twitter/LinkedIn/Reddit/Slack), решено не внедрять — нет Threads, тяжёлый стек, X вручную; забрать идеи reflection/evals.
tags: [langchain, social-media-agent, langgraph, evaluation]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-10
tier: "warm"
relevance: 0.73
source: daily/2026-08-10.md
last_accessed: 2026-08-11
---

# langchain social-media-agent — полный агент, не для нас, но идеи reflection/evals

## Что это
- **social-media-agent** от langchain-ai (LangGraph, TypeScript + немного Python/Slack): агент, который берёт URL → генерит пост для Twitter/LinkedIn → human-in-the-loop (HITL) аппрув → публикация.
- Стек: LangGraph server, Anthropic (LLM), FireCrawl (скрейпинг, 500 бесплатных кредитов), Arcade (OAuth для соцсетей), LangSmith, Supabase (опц.), Slack-интеграция.
- Twitter — через **официальный API** (OAuth 1.0a, TWITTER_API_KEY и т.д., dev-аккаунт) — НЕ куки, НЕ браузер.
- Платформы: Twitter, LinkedIn, Reddit, Slack. **Threads нет.**
- Агенты: generate-post, generate-thread, repurposer, reflection, upload-post, verify-links/verify-tweet/verify-reddit-post, curate-data, find-and-generate-images, generate-report, supervisor.
- Фичи: дедуп URL (Used URLs store в LangGraph store, SKIP_USED_URLS_CHECK), рефлексия поста перед публикацией, evals (src/evals/ — e2e, twitter, youtube, github).
- Склонирован в `data/tools/langchain-sma` (4.7M).

## Почему НЕ внедряем как есть (10.08.2026)
1. **Платформы**: главный канал владельца — Threads (а здесь его нет вообще); X — постинг вручную (403 code 64, апелляция), а тут нужен Twitter dev-аккаунт + API (писать = платный тариф).
2. **Тяжёлый стек**: отдельный LangGraph server + FireCrawl + Arcade + Supabase — это второй конвейер рядом с нашим (iva-news → черновики → TG/Threads), а не замена.
3. HITL-аппрув у нас уже есть (черновики → подтверждение владельца).

## Что можно забрать идеями
- **Reflection-агент** (саморевью поста перед публикацией) — частично есть в gstack (Review) и кураторах; можно усилить.
- **Used URLs дедуп** — у нас аналог (SENT-пометки в конвейере новостей).
- **Evals-харакнесс** (`src/evals/`) — оценивать качество наших черновиков ретроспективно.

## Если владелец захочет попробовать
- Разворачивать только на отдельной машине/контейнере: yarn install, .env (Anthropic + FireCrawl + Arcade), LangGraph server, auth через `yarn start:auth`.

## Related
- [[cards/notes/x-use-репозиторий-браузерная-автоматизация-x-не-для-нас]]
- [[cards/decisions/x-аккаунт-trampampamagi-заблокирован-апелляция-подана]]
