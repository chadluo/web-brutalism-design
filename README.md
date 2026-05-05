# web-brutalism

A Claude Code skill for building UIs using browser-native default styles.

Brutalism in web design means letting the browser's native rendering be the default — form controls, typography, and interactive elements unstyled by default, only overriding spacing and layout where needed. The result adapts automatically to the user's OS theme, font size, contrast preferences, and accessibility settings.

## Install

```
/install-skill github:y/web-brutalism-design
```

## What it covers

- Philosophy: form follows function, override only what serves a purpose
- Minimal CSS baseline (`color-scheme: light dark` + `box-sizing`)
- HTML element catalog — native interactive elements, form structure, typography
- Acceptable overrides: spacing, layout (flex/grid)
- Prohibited overrides: color, font-family, font-size on semantic elements, border-radius
- Settings panel patterns using `fieldset`/`legend`/`details`/`summary`
- Accessibility: why native elements give it for free
