---
type: "note"
description: "Интерпретация астропрогноза: Antigravity отвалил регион, в astro-interpret.py добавлен фолбэк на codex (gpt-5.6-luna), проверен живьём 19.09."
tags: ["astro","astro-interpret","agy","codex","fallback","pipeline"]
status: "active"
confidence: "EXTRACTED"
created: "2026-09-19"
source: "daily/2026-09-19.md"
domain: "work"
updated: "2026-09-20"
last_accessed: "2026-09-20"
tier: "active"
relevance: 0.97
---

# Астро-интерпретация: fallback agy → codex (19.09.2026)

Скрипт data/custom/scripts/astro-interpret.py делает человеческую интерпретацию сырого астропрогноза (после daily-astro) и шлёт владельцу.

2026-09-19: прогноз сегодня пришёл только сырой (iva-astro 07:00 — ок), интерпретация 07:10 упала: agy (Antigravity) — «not eligible… not available in your location», регион отвалили (вторая волна после 18.09). Починено: добавлен fallback в astro-interpret.py — если agy пуст, тот же промпт уходит в codex exec (gpt-5.6-luna, effort low, подписка ChatGPT). Проверено живьём: --dry вернул текст, полный прогон отправил прогноз в Telegram. Внимание: Antigravity теперь мёртв и для пула iva-write — пул едет дальше на codex (terra/luna), платный RouterAI остаётся резервом.

## Related

- [[cards/notes/астро-гороскоп-починка-и-защита-от-повтора]]
- [[cards/projects/iva-write-пул-исполнителей-подписки]]
- [[cards/notes/_index]]

## Log

- 2026-09-20:
  Скрипт data/custom/scripts/astro-interpret.py делает человеческую интерпретацию сырого астропрогноза (после daily-astro) и шлёт владельцу.
  
  2026-09-19: прогноз пришёл только сырой (iva-astro 07:00 — ок), интерпретация 07:10 упала: agy (Antigravity) — «not available in your location», регион отвалили (вторая волна после 18.09). Починено: добавлен fallback в astro-interpret.py — если agy пуст, тот же промпт уходит в codex exec (gpt-5.6-luna, effort low, подписка ChatGPT). Проверено живьём: --dry вернул текст, полный прогон отправил прогноз в Telegram. Antigravity мёртв и для пула iva-write. Фолбэк сработал автоматически на следующий день по расписанию 07:10.
