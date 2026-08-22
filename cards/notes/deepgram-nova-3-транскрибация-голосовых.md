---
type: note
description: >-
  Транскрибация голосовых владельца: Deepgram модель nova-3, язык multi, punctuate+smart_format; вызывается из agent/transcribe.ts; не верифицирует говорящего (только диаризация).
tags: [deepgram, transcription, voice, inbound, infra]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-13
source: daily/2026-08-13.md
last_accessed: 2026-08-14
tier: "warm"
relevance: 0.865
---

# Deepgram nova-3 — транскрибация голосовых

Голосовые владельца транскрибируются **Deepgram, модель nova-3** (вопрос 15:58–16:00, 12.08.2026).

- Параметры: `language=multi` (автоопределение языка, у владельца русский), `punctuate=true`, `smart_format=true` (цифры/даты/время приводятся к нормальному виду).
- Вызов из `agent/transcribe.ts`: голосовое → сырые байты → `api.deepgram.com/v1/listen?model=nova-3&language=multi` → текст.
- Inbound-пайплайн: голосовое сохраняется в `vault/attachments/`, транскрибируется, текст попадает в контекст как `[voice] ...` перед сообщением.

**Ограничение nova-3:** это ASR, не speaker verification. Умеет только диаризацию (сколько говорящих и когда кто говорит), но НЕ привязывает голос к личности — «это Антон или чужой» не отличает. Voice-gating (реагировать только на голос владельца) возможен отдельным слоем: эталон голоса → speaker embedding (напр. SpeechBrain ECAPA-TDNN, бесплатно) → косинусная близость с порогом (~0.5–1 сек на обработку). По факту вход уже ограничен приватным чатом TG — атака возможна только при доступе к аккаунту.

## Related

- [[cards/notes/raw-инбокс-vault-обработка-входящих]]
