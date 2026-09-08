---
type: "decision"
description: "Движок можно переключать на Gemini через официальный OpenAI-совместимый слой Google (ключ GEMINI_API_KEY); Antigravity CLI как движок не годится — не отдаёт tool-calls."
tags: ["gemini","provider","engine","antigravity","infra"]
status: "active"
confidence: "EXTRACTED"
domain: "work"
created: "2026-09-01"
source: "daily/2026-09-01.md"
last_accessed: "2026-09-02"
tier: "active"
relevance: 0.895
---

# Gemini как провайдер движка Ивы

Владелец попросил (01.09.2026) сделать Gemini доступным как выбор движка: токены RouterAI на исходе, а подписка Gemini у него есть.

Что сделано: провайдер `gemini` добавлен в движок — `agent/lib/model-provider.ts` (имя + дефолты), `agent/provider.ts` (baseURL `https://generativelanguage.googleapis.com/v1beta/openai`, ключ `GEMINI_API_KEY`, окно 1M), `scripts/lib/model-catalog.ts` (кнопки /model и мастер). Тесты обновлены и проходят: 38 + 31. Дефолтная модель `gemini-3.7-flash`, зрение — та же модель (Gemini мультимодальна, отдельной vision-переменной нет, как у codex).

Проверенный факт: Antigravity CLI (`agy`) движком быть НЕ может. У него нет HTTP-эндпоинта и нет способа принять внешние инструменты — в `agy --help` только текстовый print-режим и `--json-schema`. Движок Ивы требует OpenAI tool-calls каждый ход, поэтому на agy агент остался бы без инструментов. Antigravity остаётся бесплатным «писателем» в `iva-write` (там же его модели, включая gemini-3.7).

Второй проверенный факт: подписка Google AI Pro/Ultra НЕ даёт API-ключ для внешних приложений — она поднимает лимиты внутри AI Studio. Ключ для API берётся отдельно в AI Studio, у Gemini API есть свой бесплатный тариф с квотами. То есть «использовать подписку как движок» напрямую нельзя; нужен ключ.

Пока ключ не вписан, провайдер бездействует: MODEL_PROVIDER остаётся routerai.
