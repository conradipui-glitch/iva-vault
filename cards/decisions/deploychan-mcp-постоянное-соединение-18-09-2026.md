---
type: "decision"
description: "Decision: deploychan MCP (база знаний KISA по вайб-кодингу, read-only) подключён 18.09 как постоянное соединение в custom-слое; 7 инструментов; активация после /restart."
tags: ["mcp","deploychan","kisa","vibe-coding","connection"]
status: "active"
confidence: "EXTRACTED"
domain: "work"
created: "2026-09-19"
source: "daily/2026-09-19.md"
last_accessed: "2026-09-19"
tier: "active"
relevance: 0.985
---

# deploychan MCP — постоянное соединение (18.09.2026)

18.09.2026 владелец прислал https://mcp.deploychan.webcam/mcp с формулировкой «подключи и используй — пригодится». Подключено как постоянное MCP-соединение: файл data/custom/agent/connections/deploychan.ts (custom-слой, переживёт обновления), разрешены все 7 инструментов — search_knowledge, get_item, list_skills, get_skill, onboard, next_step, list_recommended; проект пересобран (npm run build). Для активации нужен перезапуск Ивы (/restart делает владелец); до него база доступна прямым HTTP.

deploychan — публичная read-only база знаний KISA по вайб-кодингу: заметки, готовые скиллы, маршруты обучения; инструментов для озвучки/медиа-обработки там нет, только справочники. Найдено 18.09 и взято на вооружение: знание agent-voice (рекомендации TTS-провайдеров — ElevenLabs: качество, 29 языков включая русский; Groq: дёшево и быстро) и скилл elevenlabs-living-voice (методика «живой» озвучки под Eleven v3 и Multilingual v2: дыхательные блоки, audio-теги, настройки голоса).

## Related

- [[cards/decisions/_index]]
- [[cards/notes/deepgram-nova-3-транскрибация-голосовых]]
- [[cards/notes/озвучка-youtube-конвейер-iva-yt]]
