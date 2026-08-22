---
type: note
description: >-
  nuwa-skill установлен как кастомный скилл eve (адаптирован под eve: пути, инструменты, ресёрч-скиллы, Agentic Protocol). Ждёт согласования тарифа перед первым прогоном.
tags: [nuwa, skill-factory, distillation, persona, custom-skill, installed]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-10
source: daily/2026-08-10.md
updated: 2026-08-10
tier: "warm"
relevance: 0.82
last_accessed: 2026-08-11
---

# nuwa-skill — фабрика персональных скиллов (distill person → skill)

## Что это
- **女娲 · Skill造人术** (alchaincyf/nuwa-skill, 67M, MIT): фабрика персона-skill'ов. Ввод = имя/тема/размытая потребность → выход = готовый `[person]-perspective/SKILL.md` (~400-500 строк).
- **Суть**: не копия человека, а «познавательная ОС»:心智模型 (3-7), decision heuristics (5-10), expression DNA, ценности/анти-паттерны, внутренние противоречия, интеллектуальная родословная, честные границы.
- **Конвейер**: Phase 0 вход → 0.5 каталог → **1: 6 параллельных agent'ов** (writings, conversations, expression, external views, decisions, timeline) каждый пишет `references/research/0X-*.md` → 1.5 CHECKPOINT ревью → 2 синтез (extraction-framework.md: triple validation — cross-domain, generativity, exclusivity) → 2.5 CHECKPOINT → 3 сборка по skill-template.md → **4 верификация: независимый subagent (sanity/edge/voice tests), FIDELITY.md scorecard** (позиции 30/20/20/15/15) → 5 двух-агентный polish.
- **Встроенные утилиты**: `scripts/download_subtitles.sh`, `srt_to_transcript.py`, `merge_research.py`, `quality_check.py` (6 критериев PASS/FAIL).
- **В комплекте 14 готовых примеров**: munger, feynman, taleb, naval, paul-graham, karpathy, ilya, elon, jobs, trump, mrbeast, sun-yuchen, zhangxuefeng, zhang-yiming, x-mastery-mentor. Каждый ~200-500KB, с references/research/.
- **Ключевые принципы**: «HOW they think, not WHAT they said»; трижды верифицируй цитаты (никаких фальшивых); не игнорируй критику (Agent 4 = анти-fanfilter); честная граница лучше выдуманной полноты; блэклист источников: Zhihu/WeChat/baike; китайские личности → Bilibili/小宇宙/36Kr.
- **Анти-паттерны**: никогда не сочинять слова; не упаковывать общие места в «уникальное мнение»; не запускать дорогой прогон без подтверждения цены; отсекать при контексте; проверять точки входа как не-блокирующие.

## Применимость к нам (10.08.2026)
1. **Прямой кейс**: «кураторский» MIMO-вариант и карточка `curator-threads` — это ровно то же, что делает nuwa: собрать формулу алгоритма Threads + стиль владельца → рабочий перспективный скилл.
2. **Как инструмент**: можно установить nuwa как скилл для будущих дистилляций (например, «сделай скилл-перспективу Талеба» для чтения новостей глазами Талеба — свежий угол для контента).
3. **Техническое**: требует 6 параллельных agent'ов + большой контекст (до 500k токенов на полный прогон), имеет fallback на серийный режим. Полный прогон дорогой — нужен выбор «быстрый/стандарт/глубокий» и подтверждение цены до старта.

## Склонирован
- `data/tools/nuwa-skill` (67M, включая 14 примеров + promo-видео).

## Решение
- **Не ставим в основной набор 15 скиллов** (это не «скилл в один файл», а целый конвейер). Держим как резерв/инструмент по запросу владельца.
- Если владелец захочет «перспективу» для контента или куратора — сначала предложить nuwa-подход, согласовать цену (token-расход) и только потом запускать.

## Related
- [[cards/notes/langchain-social-media-agent-полный-агент-не-для-нас-но-идеи]]
- [[cards/notes/x-use-репозиторий-браузерная-автоматизация-x-не-для-нас.md]]
- [[cards/notes/langchain-social-media-agent-полный-агент-не-для-нас-но-идеи.md]]
## Log
- 2026-08-10: 10.08.2026: владелец в голосовом (voice-123158.ogg) одобрил установку и адаптацию nuwa под нас. Скилл установлен в data/custom/agent/skills/nuwa-skill/ (SKILL.md адаптирован под eve: пути, инструменты web_search/web_fetch/agent/planner, ресёрч-скиллы agent-reach-reader/x-reader/youtube-transcript/news-store/web-research; убран Z-Library; добавлен Agentic Protocol). Тариф первого прогона не согласован — спросить (быстрый/стандарт/глубокий). Сборка (npm run build) и iva restart — только после явного ОК владельца.
