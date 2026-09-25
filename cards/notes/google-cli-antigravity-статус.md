---
type: note
description: "25.09: гео-блок Antigravity разобран: проверка по IP на стороне Google (hosting/proxy отсекается); бесплатные прокси не годятся; рекомендация — RouterAI."
tags: ["google","cli","tools","setup","antigravity","image-generation","pool","ops","region-block","proxy"]
status: active
confidence: "INFERRED"
domain: work
created: 2026-08-10
source: "daily/2026-08-10.mdtier: active"
last_accessed: 2026-08-10
tier: "cold"
relevance: 0.295
updated: "2026-09-26"
---
# Google CLI / Antigravity: статус

Статус Google-инструментов (актуально на 20.09.2026): генерация изображений и текстов через Google мертва. Gemini CLI отвечает «клиент больше не поддерживается, переходите в Antigravity»; сам Antigravity CLI с 19.09.2026 отвалился по региону («not available in your location») — все три модели пула (Opus 4.6 Thinking, Sonnet 4.6, Gemini 3.6) недоступны. Утром 20.09 Antigravity в iva-write вернул пустые ответы. Через Google генерить нечем; картинки решено делать через ChatGPT-подписку (codex). gws (Google Workspace CLI) — по-прежнему без авторизации, решение владельца не получено.

## gws (Google Workspace CLI)
- Установлен, но авторизации НЕТ: ни клиентского ключа, ни токена; в `.env` пусто; кэш — не креды.
- Подключение ~5 мин по скиллу google-workspace: OAuth-клиент в Google Cloud console.
- Нужен для Gmail/Календаря/Drive/Таблиц. Вопрос владельцу «Поднимаем?» — без ответа.

## Antigravity CLI
- Ставился 04.08 внутри Gemini CLI (npm @google/gemini-cli@0.53.1), токен/конфиг остались, запускался (Gemini 3.6 Flash), но бинарник/бандл пропал — остался только webm_encoder.
- Отдельного пакета @google/antigravity-cli нет → переустановка + новый OAuth.
- Упоминание Antigravity 08.08 — новость Пичая про внутреннюю платформу Google, не про сервер.

## History

- 2026-08-14: Antigravity CLI рабочий (14.08 через него переписана статья Gemini 3.7 Flash); gws не авторизован, решение владельца не получено

## Related

- [[cards/decisions/генератор-обложек-строго-chatgpt-подписка-codex]]
- [[cards/projects/iva-write-пул-исполнителей-подписки]]
- [[MOC/MOC-work|Work]]

## Log

- 2026-08-15: 14.08.2026: Antigravity CLI снова рабочий — через него Ива переписала статью-разоблачение Claude AI Ultimate через Gemini 3.7 Flash (deploy success). Ранее (09.08) Antigravity CLI был сломан (бинарник/бандл пропал после установки в Gemini CLI), требовал переустановки + нового OAuth. gws (Google Workspace CLI) — по-прежнему без авторизации, решение владельца не получено.
- 2026-09-25: 2026-09-24: Antigravity проверен вживую в 23:38 — /root/.local/bin/agy отвечает «Eligibility check failed: … not available in your location»; все 4 модели пула (opus46, sonnet46, gemini36, gemini37) мертвы, последняя попытка 17:29. Владелец голосом (23:45) спросил, можно ли поднять другой регион или бесплатные прокси — VPS технически в Нидерландах, но регион для Antigravity не поддерживается; решение не принято. Альтернативы, предложенные владельцу: оставить как есть (подписка terra/luna пишет нормально) либо пополнить RouterAI — это заодно починит эмбеддинги памяти, которые не работают с 22.09.
- 2026-09-26: 25.09.2026 (00:16) — причина гео-блока проверена живыми тестами: Antigravity гео-блокит не страну сервера (VPS в Амстердаме), проверка идёт на стороне Google по IP при вызове loadCodeAssist, и наш датацентровый IP как hosting/proxy в список разрешённых локаций не попадает. agy — Go-бинарь, честно уважает HTTPS_PROXY: запрос через прокси уходит и проверка видит внешний IP, но бесплатные публичные прокси не годятся — нестабильны (за 20 минут умерла половина), помечены как proxy/hosting, Google режет их особенно охотно. Для возврата бесплатного Opus нужен свой резидентский/мобильный IP устойчивой страны (~2–5$/мес), и даже с ним нет гарантии: региональная проверка может смотреть на страну Google-аккаунта (oauth-токен в /root/.gemini/antigravity-cli). Рекомендация Ивы: пополнить RouterAI на ~200–300₽ — закрывает и тексты, и упавший с 22.09 ночной iva-brain (эмбеддинги памяти); решение владельца не принято.
