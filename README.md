# web-brutalism

A Claude Code skill for building UIs using browser-native default styles.

Brutalism in web design means letting the browser's native rendering be the default — form controls, typography, and interactive elements unstyled by default, only overriding spacing and layout where needed. The result adapts automatically to the user's OS theme, font size, contrast preferences, and accessibility settings.

## What it covers

- **Philosophy** — form follows function; spacing and alignment are the primary design tools
- **Design brief** — establish purpose, feel, and typographic voice before writing CSS
- **Style presets** — Swiss International, Bauhaus, Editorial, Technical, Minimalist; each maps to specific system font stack categories
- **System font stacks** — all 14 categories from [modern-font-stacks.md](skills/web-brutalism/modern-font-stacks.md); no web font downloads
- **Minimal CSS baseline** — `color-scheme: light dark`, `box-sizing: border-box`, `font-size: inherit` on form elements
- **Allowed overrides** — spacing/layout (flex/grid), system color keywords, `line-height` on body, `font-weight` on labels
- **Prohibited overrides** — custom `color`/`background-color` values, web fonts, `font-size` on semantic elements, `border-radius`, `:focus { outline: none }`
- **HTML element catalog** — native interactive elements, form structure (`fieldset`/`legend`/`label`), typography, sectioning, media
- **Settings panel pattern** — `fieldset`/`legend`/`details`/`summary` with zero custom components
- **Accessibility foundation** — native elements as a head start; per-project requirements (touch targets, ARIA, `lang`) still apply
