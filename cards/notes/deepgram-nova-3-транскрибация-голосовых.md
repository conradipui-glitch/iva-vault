---
type: note
description: "Транскрибация голосовых владельца: Deepgram nova-3, language=multi. 18.09 проверено API: русского TTS в Deepgram нет и моделей ElevenLabs нет — русский только в STT."
tags: ["deepgram","transcription","voice","inbound","infra","tts","stt"]
status: active
confidence: EXTRACTED
domain: work
created: 2026-08-13
source: daily/2026-08-13.md
last_accessed: 2026-08-14
tier: "cold"
relevance: 0.415
updated: "2026-09-19"
---

# Deepgram nova-3 — транскрибация голосовых

Голосовые владельца транскрибируются **Deepgram, модель nova-3** (вопрос 15:58–16:00, 12.08.2026).

- Параметры: `language=multi` (автоопределение языка, у владельца русский), `punctuate=true`, `smart_format=true` (цифры/даты/время приводятся к нормальному виду).
- Вызов из `agent/transcribe.ts`: голосовое → сырые байты → `api.deepgram.com/v1/listen?model=nova-3&language=multi` → текст.
- Inbound-пайплайн: голосовое сохраняется в `vault/attachments/`, транскрибируется, текст попадает в контекст как `[voice] ...` перед сообщением.

**Ограничение nova-3:** это ASR, не speaker verification. Умеет только диаризацию (сколько говорящих и когда кто говорит), но НЕ привязывает голос к личности — «это Антон или чужой» не отличает. Voice-gating (реагировать только на голос владельца) возможен отдельным слоем: эталон голоса → speaker embedding (напр. SpeechBrain ECAPA-TDNN, бесплатно) → косинусная близость с порогом (~0.5–1 сек на обработку). По факту вход уже ограничен приватным чатом TG — атака возможна только при доступе к аккаунту.

## Related

- [[cards/notes/raw-инбокс-vault-обработка-входящих]]
- [[cards/notes/_index]]
- [[cards/notes/озвучка-youtube-конвейер-iva-yt]]
- [[cards/decisions/2026-09-18-deploychan-mcp-постоянное-соединение]]

## Log

- 2026-09-19:
  Голосовые владельца транскрибируются Deepgram nova-3 (language=multi, punctuate=true, smart_format=true), вызов из agent/transcribe.ts; это ASR с диаризацией, не speaker verification.
  
  Проверено по живому API ключа владельца 18.09.2026: моделей ElevenLabs в Deepgram нет — все 102 TTS-модели собственные (Aura и Aura-2). Русского в TTS нет: «мультиязыковые» у них — это два региональных варианта одного языка (напр. fr + fr-FR), а не настоящая полилингвальность; языки всех голосов — en, de, es, fr, it, ja, nl, фильтр Russian в TTS пустой. Русский есть только в STT — 18 моделей, включая nova-3 и nova-2. Для русской озвучки (дубляж) Deepgram не подходит: синтез на русском — Fish Audio, ElevenLabs или Groq (последние два подтверждаются базой знаний deploychan).
