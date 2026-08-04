---
type: decision
description: >-
  Автопроверка комментариев под постами @toharo_pro на токсичность каждый день ~10:00 Asia/Omsk; кандидаты на скрытие приходят владельцу, скрытие только после его «ок» (need_approval)
tags: [threads, moderation, automation, telegram]
status: active
confidence: EXTRACTED
domain: personal
created: 2026-08-04
source: daily/2026-08-04.md
last_accessed: 2026-08-05
tier: active
relevance: 1.0
---

# Ежедневная проверка комментариев Threads

## Решение (2026-08-04)
- Владелец выбрал режим **need_approval**: ежедневно присылать кандидатов на скрытие, скрывать только после его явного «ок».
- Настроено: systemd user-таймер `iva-comment-check.timer` → `iva-comment-check.service` (oneshot), `OnCalendar=*-*-* 10:00:00 Asia/Omsk`, `Persistent=true`.
- Скрипт: `/root/iva/scripts/threads-comment-check.ts` (самодостаточный промпт, без load_skill — скилл не в сборке .output; таймаут 300 с, чтение result.message, логирование).
- Доставка: `sendTelegramHtml` из `scripts/lib/telegram-send.mjs` в чат владельца.
- Скилл `/root/iva/agent/skills/threads-comment-check/SKILL.md` создан, но НЕ попадёт в рантайм до `npm run build` + рестарта (eve читает скиллы из `.output/`).
- Первый прогон: 2026-08-04 11:40 UTC+2 — статус waiting, «Сегодня чисто ✅», отправлено в Telegram, сервис Finished.
- Проверка через браузер: agent-browser сессия `thc` (Threads залогинен), посты ≤7 дней.

## Запреты
- Скрипт/агент никогда не скрывает, не блокирует, не рестриктит и не отвечает — только отчёт.
- «Hide for everyone» прячет конкретный комментарий; «Restrict» ограничивает автора (его комментарии под постами видит только он); блокировка — только по команде владельца.
