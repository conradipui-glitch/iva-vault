---
type: note
description: >-
  14.08.2026 разоблачение фейкового репозитория wallquailrespect/claude-ai-ultimate (~370 звёзд, 0 форков): README-пустышка, ссылки ведут на shady-портал softhvn.xyz с «установщиками», накрученные звёзды, кликбейт-темы. Статья на сайт переписана через Gemini 3.7 Flash (Antigravity CLI), деплой success.
tags: [scam, github, security, claude, toharo-lab, gemini-3-7]
status: active
confidence: EXTRACTED
domain: knowledge
created: 2026-08-15
source: daily/2026-08-15.md
last_accessed: 2026-08-16
tier: "warm"
relevance: 0.85
---

# claude-ai-ultimate-фейковый-репозиторий-разбор

14.08.2026: репозиторий `wallquailrespect/claude-ai-ultimate` попал в подборку новостей (набирал просмотры); разбор через Grok показал типичный фейковый проект:

- Почти нет кода: только README.md и index.ts из 6 строк («Running…» и выход).
- README рекламирует «Claude AI Ultimate» (all-in-one: текст, картинки, аудио, видео, prompt-библиотека); все ссылки на «документацию» и «скачать релиз» ведут на claude-ai-ultimate.softhvn.xyz.
- softhvn.xyz — shady download-портал: «Claude AI Ultimate for Windows», TeamViewer Toolkit, Sony Vegas Boost, ExitLag Plus и т.п.; «VirusTotal verified 100% safe» — стандартный маркетинговый приём мошенников.
- ~370 звёзд, 0 форков, 0 вотчеров — классический признак накрутки.
- Topics кликбейтные: anthropic-leak, claude-4-6-opus, claude-opus-5, code-leak — ловят ищущих «сливы».
- Опасность: сейчас ходят кампании с фейковыми установщиками Claude (malware через поддельные сайты, артефакты Claude).

Статья-разоблачение на сайт (категория выбрана Ивой): переписана через Gemini 3.7 Flash в Antigravity CLI, заголовок «Claude AI Ultimate»: как хайповый репозиторий дня превращается в ловушку; открытие цепляющим вопросом; нарратив вайб-кодинг → доверие к социальным сигналам → разбор прецедента → «анатомия накрутки и воронка слива». Накрутка и пустышка — факт; кража данных/ботнет/криптокошельки поданы как гипотеза и класс угроз (владелец сам сказал «предполагаю»). Ссылка: https://conradipui-glitch.github.io/toharo-lab/blog/claude-ai-ultimate-scam/

## Related

- [[cards/projects/сайт-toharo-lab-функционал-статей-оглавление-rss-обсудить-в-]]
- [[cards/notes/google-cli-antigravity-статус]]
