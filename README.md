# Anti AI Slop

Плагин для ZCode, который отучает любые модели от «AI-слопа» — фирменных признаков
нейросетевого кода и дизайна — если ты явно не попросил конкретную вещь.

Работает через два механизма: SessionStart-хук вливает компактные правила в контекст
каждой сессии, а скилл `anti-ai-slop` разворачивает полный свод на задачах кода и дизайна.
Команда `/anti-slop:check` прогоняет файлы или недавние изменения по всем правилам и
исправляет найденное.

## Что запрещено по умолчанию

Дизайн и UI:
- фиолетово-синие градиенты (`#8B5CF6`, `#7C3AED` и соседи), неоновые свечения, градиентный текст
- шрифт Inter как «выбор»
- эмодзи в интерфейсе, кнопках, заголовках и консольном выводе
- глассморфизм и blur-эффекты на каждом углу
- одинаковые карточные сетки, `rounded-2xl` на всём
- шаблонный лендинг hero + 3 карточки + pricing
- копирайт-клише «Streamline your workflow», «Supercharge your…»

Код:
- комменты-пересказ очевидного, эмодзи в комментах, секционные баннеры
- защитный бойлерплейд: try/catch, который не может сработать, null-чеки невозможных null
- непрошеные фичи, фреймворки и абстракции «на будущее»
- регенерация файлов вместо точечных правок
- игнорирование стиля окружающего кода

Словарь: robust, seamless, comprehensive, delve, leverage, tapestry, testament, harness,
unlock, pivotal, «it's worth noting» и прочее — под запретом.

Явный запрос снимает запрет: «сделай фиолетовый градиент» — будет градиент, без нытья.
«Сделай красиво» и «современно» ничто не снимают.

## Установка (ZCode Desktop)

1. **Plugin Marketplace → Add → Add Plugin Marketplace**
2. Вставь адрес этого репозитория: `https://github.com/artnovaafk/anti-ai-slop`
3. Установи плагин **Anti AI Slop** из появившегося маркета.

Проверка: открой новый чат и попроси лендинг для кофейни — в результате не должно быть
фиолетовых градиентов, Inter и эмодзи в UI.

## Если хост не ZCode

- Скилл: скопируй `anti-ai-slop/skills/anti-ai-slop` в `~/.claude/skills/` или общий
  `~/.agents/skills/`.
- Всегда-на правила: содержимое `anti-ai-slop/hooks/rules/always.md` вставь в свой
  AGENTS.md / CLAUDE.md / системный промпт — хук `${CLAUDE_PLUGIN_ROOT}` сработает только
  внутри плагинного механизма.

## Состав

```
marketplace.json                     — каталог маркетплейса для установки из репозитория
anti-ai-slop/.zcode-plugin/plugin.json — манифест плагина
anti-ai-slop/skills/anti-ai-slop/SKILL.md — полный свод правил
anti-ai-slop/hooks/hooks.json        — SessionStart-хук
anti-ai-slop/hooks/rules/always.md   — компактные правила для каждой сессии
anti-ai-slop/commands/check.md       — команда /anti-slop:check
```

## Как править

Редактируй `anti-ai-slop/skills/anti-ai-slop/SKILL.md` (полный свод) и
`anti-ai-slop/hooks/rules/always.md` (компактная версия). После правок подними `version`
в манифесте и в `marketplace.json`, закоммить и обнови плагин через маркетплейс.

## English summary

A ZCode plugin that stops AI models from producing tell-tale "AI slop": purple/neon gradients,
the Inter font, emoji UI, glassmorphism, uniform card grids, AI vocabulary (robust, seamless,
delve, leverage…), over-commenting and defensive boilerplate. SessionStart hook injects compact
rules into every session; the `anti-ai-slop` skill carries the full rulebook; `/anti-slop:check`
audits files and fixes findings. Each ban is lifted only when the user explicitly asks for that
exact pattern. Install via Plugin Marketplace → Add → paste this repository URL.

MIT, версия 0.1.0.
