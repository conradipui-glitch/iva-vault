# Задание: перегенерировать обложки на сайте toharo-lab

## Контекст

Сайт: https://github.com/conradipui-glitch/toharo-lab (публичный)
Живой: https://conradipui-glitch.github.io/toharo-lab/

Три обложки сгенерированы через Pollinations. Нужно заменить их на GPT Image 2,
используя твой ключ. Всё остальное на сайте не трогать.

Перед работой прочитай `AGENTS.md` в корне репозитория — там правила проекта.

## Шаг 1. Клонировать (если ещё нет)

```bash
git clone https://github.com/conradipui-glitch/toharo-lab.git
cd toharo-lab
npm ci
```

Если репозиторий уже есть — `git pull`.

## Шаг 2. Положить ключ

Создай файл `.env.local` в корне репозитория:

```
OPENAI_API_KEY=<твой ключ>
OPENAI_IMAGE_MODEL=gpt-image-2
```

Если ключ от агрегатора, а не напрямую от OpenAI — добавь третьей строкой
базовый URL:

```
OPENAI_BASE_URL=<базовый URL агрегатора, например https://.../v1>
```

**Файл `.env.local` в `.gitignore` и коммититься не должен.** Репозиторий
публичный: попавший в коммит ключ считается скомпрометированным. В проекте
стоит pre-commit хук, который такой коммит остановит — не обходи его
через `--no-verify`.

Образец переменных — в `.env.example`.

## Шаг 3. Перегенерировать три обложки

Формат `cover` (16:9) — менять не нужно, он подставляется сам.
Флаг `--force` обязателен: без него скрипт не перезапишет существующий файл.

```bash
npm run cover -- --slug agents-md-pravila-dlya-agentov --provider openai --force \
  --prompt "minimalist editorial illustration, warm cream paper background, lime green accent color, a single document at center with thin lines radiating outward to several small abstract tool shapes, flat vector, geometric, generous negative space, no text, no letters, no words" \
  --alt "Один документ в центре, от которого расходятся линии к нескольким инструментам"

npm run cover -- --slug skills-claude-code-svoi-navyk --provider openai --force \
  --prompt "minimalist editorial illustration, warm cream paper background, lime green accent color, a row of simple folder shapes with one folder opening and glowing, flat vector, geometric, generous negative space, no text, no letters, no words" \
  --alt "Ряд папок, одна из которых подсвечена и раскрывается"

npm run cover -- --slug tri-sloya-nadezhnogo-agenta --provider openai --force \
  --prompt "minimalist editorial illustration, warm cream paper background, lime green accent color, three clean horizontal layers stacked with thin vertical lines connecting them, flat vector, geometric, generous negative space, no text, no letters, no words" \
  --alt "Три горизонтальных слоя, соединённых тонкими линиями"
```

### Требования к стилю

Единый визуальный язык сайта, отступать от него не надо:

- тёплый бежевый фон (как `#f7f4ec`), лаймовый акцент `#c9ff3d`;
- плоская векторная графика, геометрия, много воздуха;
- **никакого текста и букв на картинке** — сгенерированные буквы всегда кривые;
- без попыток нарисовать интерфейс или код буквально: работает абстракция.

Если картинка вышла тёмной, пёстрой или с текстом — перегенерируй, поправив
промпт. Три обложки должны выглядеть как одна серия, а не как три разных стиля.

## Шаг 4. Проверить

```bash
npm run check
npm run build
```

`check` не должен ругаться на обложки. Дополнительно глазами:

```bash
npm run dev
```

Открой http://localhost:3000 и посмотри ленту: три карточки, обложки в одном
стиле, ничего не поехало.

## Шаг 5. Опубликовать

```bash
git add public/covers/ content/posts/
git commit -m "covers: перегенерация обложек через GPT Image 2"
git push
```

После пуша GitHub Actions сам соберёт и выкатит сайт — примерно полторы минуты.
Проверь, что сборка зелёная:

```bash
gh run list --limit 1
```

Затем открой https://conradipui-glitch.github.io/toharo-lab/ и убедись, что
обложки обновились.

## Критерий готовности

- [ ] Три обложки перегенерированы через GPT Image 2, пропорции 16:9
- [ ] Стиль единый, текста на картинках нет
- [ ] `coverAlt` у всех трёх — по-русски, описывает смысл картинки
- [ ] `npm run check` и `npm run build` проходят
- [ ] Ключ в репозиторий не попал (`git log -p` не содержит `.env.local`)
- [ ] Actions зелёный, на живом сайте новые обложки

## Чего не делать

- Не трогать тексты статей, вёрстку, конфиги и `deploy/`
- Не менять slug постов — это URL
- Не коммитить `.env.local` и не обходить pre-commit хук
- Не добавлять зависимости
