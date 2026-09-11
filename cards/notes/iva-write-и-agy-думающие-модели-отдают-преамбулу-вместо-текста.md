---
type: "note"
description: "Проверенный баг: через agy ответ thinking-моделей приходит как преамбула («Let me draft...»), проверка длины в iva-write отсеивает её, пул сам уходит дальше; workaround для JSON-задач через banned-слова."
tags: ["iva-write","write-pool","agy","tools","workflow"]
status: "active"
confidence: "EXTRACTED"
domain: "work"
created: "2026-09-08"
source: "daily/2026-09-08.md"
last_accessed: "2026-09-09"
tier: "active"
relevance: 0.955
---

# iva-write и agy: думающие модели отдают преамбулу вместо текста

Проверено 08.09.2026 на задаче «3 поста одним JSON».

Симптом: gemini-3.7-flash отдаёт через agy нормальный текст, а claude-opus-4-6-thinking (и другие thinking-модели) в поле response agy-JSON отдаёт преамбулу размышлений: «Let me draft the posts...» (62–69 знаков). iva-write принимает это как готовый текст: если лимит стоит на один пост (например 480), короткая преамбула проходит проверку и пул останавливается на мусоре. Видно в data/write-pool-usage.jsonl: opus ok=true при chars=62/69.

Workaround для многопостовых задач: лимит --limit ставить на весь результат (3 поста примерно 1600), а в --banned добавить английские зачины преамбул: Let me,Let's,I'll,I will,Here is,Here are,Draft,Drafting. Тогда проверка завернёт преамбулу как «запрещённое слово» и пул сам перейдёт к следующей модели (сработало: gemini37 вернул валидный JSON). Альтернатива: --model gemini37 сразу для JSON-задач, но руками модель выбирать нельзя, только если владелец назвал.

Признак проблемы: stdout начинается не с { и содержит английскую фразу про draft/verify при русском задании.

## Related

- [[cards/notes/формат-постов-мыслей-для-личного-ai-блога]]
