---
type: "note"
description: "B.AI провайдер подключён к Иве (OpenAI-совместимый, 48 моделей). Установка 06.09.2026, требует рестарта. Вечером 06.09 — баг панели: B.AI не появлялся в меню после рестарта, чат замолкал при выборе модели."
tags: ["bai","provider","api","model","integration"]
status: "active"
confidence: "EXTRACTED"
created: "2026-09-06"
source: "daily/2026-09-06.md"
updated: "2026-09-07"
domain: "knowledge"
last_accessed: "2026-09-07"
tier: "active"
relevance: 1.0
---

# Провайдер B.AI (Ива)

Провайдер B.AI (OpenAI-совместимый агрегатор, https://api.b.ai/v1, 48 моделей: GPT-5.x, Claude, Gemini, GLM-5.x, DeepSeek, Kimi и др.) подключён к Иве 06.09.2026.

Источник: патч от glmbot (Hermes-агент, /home/hermes-pilot), пакет patches/bai-provider. Плюс владелец подтвердил установку.

Что сделано:
- BAI_API_KEY в .env (взят из /home/hermes-pilot/.hermes/.env, 35 символов).
- Пропатчено 7 файлов: agent/lib/model-provider.ts, agent/provider.ts, scripts/lib/model-catalog.ts, scripts/lib/model-summary.ts, webapp/server.py, scripts/cli/doctor.test.ts, scripts/lib/version-update.test.ts.
- Провайдер gemini (локальная правка Iva от 01.09.2026) сохранён — патч базировался на версии с gemini.
- Мой бэкап це: /root/iva/data/custom/backup-bai-20260906-134255/.
- model-provider.test.ts синхронизирован под добавленный bai (3 списка). Тесты: 127/127 ок, npm run build собран.

Особенности:
- BAI_REASONING_LEVELS — по-модельная матрица уровней в agent/provider.ts (glm-5.3-flash не поддерживает minimal/xhigh; gpt-5.2/5.5 не поддерживает max; claude-sonnet/opus-5 не поддерживает minimal).
- baiFetch — reasoning_effort встраивается в тело запроса (как у RouterAI), совместимого поля eve нет (compatibleReasoning: false).
- Зрение: deepseek-v4-flash-vision-exp (проверено, отвечает на картинку).
- Live-проверка ключа 06.09.2026: GET /models → 200, chat/completions glm-5.3-flash → 200 с reasoning_content.

ВАЖНО: изменения вступают в силу только после перезапуска процесса. Рестарт делает владелец (iva restart / /restart), Ива сама себя не перезапускает.

## Log

- 2026-09-07: Дополнение (вечер 06.09.2026): после рестарта панель не показывала B.AI — веб-панель (iva-webapp) запускалась старой версией (процесс от 24 августа), хотя код с bai лежал в webapp/server.py с 05.09; рестарт сервиса исправил отображение. Но при выборе провайдера B.AI и модели в веб-меню модель не выбиралась, а чат переставал отвечать. Разбор обработчика /api/agent: target = prov or provider_now(), и если модель кликается до смены провайдера, каталог берётся текущего контура → 400 «модели нет в списке». При смене модели вызывается только `systemctl restart iva.service`, а iva-telegram-poll.service — нет, поэтому при зависании агента на старте канал молчит. Пара glm-5.3-flash + max валидна (API отвечает, tool calling работает), но по usage.jsonl ни одной рабочей записи на bai — фактически B.AI ни разу не отработал. Статическая причина падения iva.service не найдена — нужно живое воспроизведение. Слабые места: рестарт поллинга при смене модели + валидация модели по каталогу текущего контура.
