---
type: note
description: >-
  Оценка x-use: механики аккуратности есть (рандомные задержки 60–180с, undetected-chromedriver, прокси, валидация кук), но риск бана X не снимают — вердикт «не внедряем» подтверждён.
tags: [x-automation, x-use, mcp, decision, security]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-10
source: daily/2026-08-10.md
updated: 2026-08-10
tier: "warm"
relevance: 0.805
last_accessed: 2026-08-11
---

# x-use репозиторий — браузерная автоматизация X, не для нас

## Что это
- **x-use** (ihuzaifashoukat/x-use, v2-релонч twitter-automation-ai, MIT, Python 3.10+): MCP-сервер + CLI для автоматизации X (Twitter) через реальный браузер (Selenium + Chrome), без X API ключа.
- Авторизация — **экспорт кук** (Cookie-Editor extension). Мультиаккаунт, драфт-аппрув по умолчанию, свои LLM.
- Внутри `src/xuse/skills_pack/`: 5 скиллов (x-use, x-use-content, x-use-engage, x-use-review, x-use-setup) — все заточены на MCP-инструменты x-use.
- Склонирован в `data/tools/x-use` (2.9M). PyPI: `pip install x-use-mcp`.

## Почему НЕ внедряем (10.08.2026)
1. **Политика X**: постинг вручную (403 code 64); аккаунт @TrampampamAGI заблокирован за «inauthentic behaviors», апелляция ждёт. Автоматизация браузером через куки = прямой риск повторного бана.
2. **Политика кук** (06.08): куки X/Threads — только резерв, без использования без явной просьбы.
3. **Технически**: на VPS нет Chrome и selenium → x-use не запустится без доустановки (~сотни МБ, headless-риски).

## Что извлекли
- Скрипт `scripts/make_social_preview.py` — генератор соц-превью (1280×640, Pillow) для самого репо, не для нас.
- Контентные подходы (нишевый ресёрч → драфты по одному → ревью) уже покрыты нашими скиллами (news-editor, post-writer-sms, publish, x-algo-skill).

## Если владелец передумает
- Нужно: явное разрешение на куки-автоматизацию X + установка Chrome (или переход на локальную машину владельца), `pip install x-use-mcp`, регистрация MCP в eve.
- Тогда скиллы из skills_pack можно скопировать в `data/custom/agent/skills/` (5 шт).

## Related
- [[cards/decisions/политика-кук-threads-x-резерв-без-запросов]]
- [[cards/decisions/x-аккаунт-trampampamagi-заблокирован-апелляция-подана]]
## Log
- 2026-08-10:
  Повторный анализ кода (10.08) подтвердил: x-use написан аккуратно, не «грязный спам-тул». Rate limiting — случайные задержки 60–180 сек между действиями (random.uniform), для лайков вдвое короче, настраивается per-action. Stealth — опция use_undetected_chromedriver, конфигурируемый user-agent, per-account прокси с пулами и проверкой в doctor. Куки — валидация формата Cookie-Editor, обязательны auth_token + ct0, проверка на истечение, бэкап accounts.json перед мутацией. Doctor даёт PASS/FAIL/SKIP по каждому чеку.
  
  Вердикт не изменился: не внедряем. Механики аккуратности есть, но не устраняют риск бана — undetected-chromedriver детектится X по сигнатурам WebDriver, а @TrampampamAGI уже забанен за «inauthentic behaviors» (апелляция ждёт), второй бан = конец. Chrome на VPS нет (доустановка ~300МБ + headless-риски). Политика кук (06.08): только резерв, без явной просьбы владельца не используем. Наш X-постинг вручную (403 code 64) — осознанное решение.
  
  Пересмотр возможен только по явной просьбе владельца + разрешение на куки-автоматизацию + Chrome (или локальная машина владельца) + pip install x-use-mcp + регистрация MCP. Тогда 5 скиллов из skills_pack/ копируются в data/custom/agent/skills/.
