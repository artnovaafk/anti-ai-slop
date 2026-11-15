# Anti AI Slop

![version](https://img.shields.io/badge/version-0.1.0-2ea44f)
![license](https://img.shields.io/badge/license-MIT-2ea44f)
![host](https://img.shields.io/badge/ZCode-Desktop%20plugin-2ea44f)
![i18n](https://img.shields.io/badge/rules-EN-2ea44f)

Плагин для ZCode, который отучает любые модели от «AI-слопа» — фирменных признаков
нейросетевого кода и дизайна. Нейросети рисуют один и тот же лендинг: фиолетовый градиент,
шрифт Inter, три одинаковые карточки, 🚀 в кнопке — и пишут код с комментами-пересказом
и `try/catch`, который не может сработать. Этот плагин ставит на всё это запрет по умолчанию.

Работает через два механизма: SessionStart-хук вливает компактные правила в контекст каждой
сессии, а скилл `anti-ai-slop` разворачивает полный свод на задачах кода и дизайна. Команда
`/anti-slop:check` прогоняет файлы или недавние изменения по правилам и исправляет найденное.

> **Явный запрос снимает запрет**: «сделай фиолетовый градиент» — будет градиент, без нытья.
> «Сделай красиво» и «современно» — ничто не снимают.

---

## Что запрещено по умолчанию

### Дизайн и UI

| Запрещено | Вместо |
|---|---|
| фиолетово-синие градиенты (`#8B5CF6`, `#7C3AED`, `#6366F1`), неон, `bg-clip-text` | один сдержанный акцент под тему, плоские заливки |
| шрифт Inter как «выбор» | шрифт проекта или характерный для темы |
| эмодзи в UI, кнопках, заголовках, консоли | текст; эмодзи только по явному запросу |
| глассморфизм и `backdrop-blur` на каждом углу | плотные поверхности, 1px рамки, честные тени |
| одинаковые карточные сетки, `rounded-2xl` на всём | живая сетка: акценты, списки, таблицы, асимметрия |
| шаблонный лендинг hero + 3 карточки + pricing | вёрстка от контента и предмета |
| копирайт «Streamline your workflow», «Supercharge…» | конкретика: что продукт реально делает |

### Код

| Запрещено | Вместо |
|---|---|
| комменты-пересказ (`# инкремент`, «This function…», баннеры) | коммент только для неочевидного *why* |
| `try/catch`, который не может сработать; null-чеки невозможных null | обработка реальных ошибок в идиоме проекта |
| непрошеные фичи, фреймворки, абстракции «на будущее» | минимальное корректное изменение |
| регенерация всего файла | точечные правки соседнего кода не трогаются |
| собственный стиль вопреки проекту | сначала прочитать окружающий код и повторить его |

### Словарь

`robust`, `seamless`, `comprehensive`, `leverage`, `delve`, `tapestry`, `testament`,
`harness`, `unlock`, `elevate`, `pivotal`, `game-changer`, «it's worth noting» — не
использовать. Писать plainly: что код делает и при каких условиях работает. «Robust» →
«ретраит 3 раза, потом падает громко».

---

## Установка (ZCode Desktop)

1. **Plugin Marketplace → Add → Add Plugin Marketplace**
2. Вставь адрес репозитория: `https://github.com/artnovaafk/anti-ai-slop`
3. Установи плагин **Anti AI Slop** из появившегося маркета.

Проверка: открой новый чат и попроси лендинг для кофейни — в результате не должно быть
фиолетовых градиентов, Inter и эмодзи в UI.

<details>
<summary><strong>Если хост не ZCode</strong></summary>

- **Скилл**: скопируй `anti-ai-slop/skills/anti-ai-slop` в `~/.claude/skills/` или общий
  `~/.agents/skills/`.
- **Всегда-на правила**: содержимое `anti-ai-slop/hooks/rules/always.md` вставь в свой
  AGENTS.md / CLAUDE.md / системный промпт — хук `${CLAUDE_PLUGIN_ROOT}` сработает только
  внутри плагинного механизма.

</details>

<details>
<summary><strong>Состав репозитория</strong></summary>

```
marketplace.json                                — каталог: установка по URL репозитория
anti-ai-slop/.zcode-plugin/plugin.json          — манифест плагина
anti-ai-slop/skills/anti-ai-slop/SKILL.md       — полный свод правил
anti-ai-slop/hooks/hooks.json                   — SessionStart-хук
anti-ai-slop/hooks/rules/always.md              — компактные правила для каждой сессии
anti-ai-slop/commands/check.md                  — команда /anti-slop:check
```

</details>

## Как править

Редактируй `anti-ai-slop/skills/anti-ai-slop/SKILL.md` (полный свод) и
`anti-ai-slop/hooks/rules/always.md` (компактная версия). После правок подними `version`
в манифесте и в `marketplace.json`, закоммить — обновление придёт тем, кто добавил репо
как маркетплейс.

---

## English summary

A ZCode plugin that stops AI models from producing tell-tale "AI slop": purple/neon gradients,
the Inter font, emoji UI, glassmorphism, uniform card grids, AI vocabulary (*robust*, *seamless*,
*delve*, *leverage*…), over-commenting and defensive boilerplate. A SessionStart hook injects
compact rules into every session; the `anti-ai-slop` skill carries the full rulebook;
`/anti-slop:check` audits files and fixes findings. Each ban is lifted only when the user
explicitly asks for that exact pattern. Install: Plugin Marketplace → Add → paste this
repository URL.
