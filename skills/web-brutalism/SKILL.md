---
name: web-brutalism
description: >
  Web brutalism design guide: how to build UIs using browser-native default styles. Use this skill
  whenever the user is designing or building a new web page, UI component, browser extension popup,
  settings panel, or any frontend interface — especially when they want a minimal, functional, or
  "native" aesthetic. Also trigger when the user mentions brutalism, "browser defaults", "no custom
  styles", "native HTML", or wants to avoid over-styling. Covers philosophy, HTML element selection,
  and acceptable CSS overrides.
---

## Philosophy

Brutalism in architecture means materials are left in their raw, functional state — concrete is
concrete, steel is steel. Nothing is hidden. In web design, the same principle applies: **let the
browser's native rendering be the default, and only override what serves a functional purpose.**

The browser already has a complete visual language: heading hierarchy, form controls that match the
OS, interactive states (focus, hover, checked, disabled), accessible defaults, and automatic
adaptation to the user's system preferences (dark mode, font size, contrast). Overriding these is
work that must pay for itself.

The principle: **if a property override is purely decorative, remove it.**

Acceptable overrides:
- Spacing: `margin`, `padding`, `gap`, `width`, `max-width`
- Layout: `display: flex/grid`, `flex-direction`, `align-items`, `justify-content`, `grid-template-*`
- Functional sizing: `min-width`, `max-height`, `flex: 1`, `flex-shrink`
- Utility: `box-sizing: border-box`, `cursor: pointer`, `overflow`, `white-space`

Do not override:
- `color`, `background-color` — breaks dark mode, contrast preferences, high-contrast mode
- `font-family` — overrides the user's system font choice
- `font-size` on semantic elements (h1–h6, p, small, etc.) — destroys the browser's typographic scale
- `border-color`, `border-radius`, `outline` — decorative; breaks focus visibility
- `text-transform`, `letter-spacing`, `font-weight` on semantic elements — decorative

## The Minimal CSS Baseline

The only universal rule needed:

```css
:root {
  color-scheme: light dark;
}

*, *::before, *::after {
  box-sizing: border-box;
}
```

`color-scheme: light dark` is essential — it tells the browser to render all native controls
(buttons, inputs, scrollbars, system colors like `Canvas`, `CanvasText`, `GrayText`) in the user's
preferred color scheme automatically. Without it, form controls may not adapt to dark mode.

Do **not** add a CSS reset. Resets are the opposite of this approach — they erase the browser's
defaults and force you to rebuild everything.

## HTML Elements as Functional Tools

The full element list is at https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements.
Before reaching for a `<div>` + JavaScript, check if a native element already does the job.

### Interactive without JavaScript

| Element | What it does natively |
|---|---|
| `<details>` / `<summary>` | Collapsible disclosure widget — no JS accordion needed |
| `<dialog>` | Modal/popover — `dialog.showModal()` handles focus trapping, backdrop, Escape key |
| `<input type="range">` | Slider with min/max/step |
| `<input type="color">` | Color picker |
| `<input type="date/time/datetime-local">` | Date/time picker |
| `<select>` / `<datalist>` | Dropdown or autocomplete |
| `<progress>` / `<meter>` | Progress bar and measurement gauge |

### Form structure

Use `<fieldset>` + `<legend>` to group related controls. This gives semantic grouping, visual
grouping (native border), and accessibility (screen readers announce the group name) with zero CSS.

Use `<label>` wrapping its control rather than `for`/`id` pairing — simpler, and the entire label
area becomes a click target.

### Typography hierarchy

Let the browser scale do the work. `<h1>`–`<h6>` already have a meaningful size progression.
`<strong>` and `<em>` already have weight and style. `<code>`, `<kbd>`, `<samp>`, `<var>` already
use monospace. `<blockquote>` already has indentation. `<small>` already reduces size.

Override `font-size` only when you need a fixed layout constraint (e.g., a 360px popup where
default `h1` is too large) — and do it sparingly.

### Lists and description lists

`<dl>` / `<dt>` / `<dd>` is underused. It's the right element for key-value pairs, settings rows,
metadata, glossaries. No table needed.

### Sectioning

`<section>`, `<article>`, `<nav>`, `<aside>`, `<header>`, `<footer>`, `<main>` provide document
structure that assistive technology understands. Use them over `<div>` wherever they apply. They
have no visual effect by default — add only the spacing you need.

### Media

`<figure>` + `<figcaption>` provides semantically captioned media with a native indented block
style. `<picture>` with `srcset` handles responsive images without JS.

`<details>` inside a `<figure>` creates an expandable media description, entirely in HTML.

## Building a Settings Panel

The `<details>`/`<summary>` + form controls pattern covers most settings UIs:

```html
<form>
  <fieldset>
    <legend>Display</legend>

    <label>
      <input type="checkbox" name="darkMode"> Dark mode
    </label>

    <label>
      Columns
      <input type="range" name="columns" min="1" max="4" value="2">
    </label>

    <label>
      Theme
      <select name="theme">
        <option>System</option>
        <option>Light</option>
        <option>Dark</option>
      </select>
    </label>
  </fieldset>

  <details>
    <summary>Advanced</summary>
    <fieldset>
      <legend>Developer</legend>
      <label><input type="checkbox" name="debug"> Debug mode</label>
    </fieldset>
  </details>

  <button type="submit">Save</button>
</form>
```

Only spacing CSS needed to make this usable. No custom component library.

## Spacing Without Overriding Appearance

When adding layout CSS, use a flat `display: flex` or `display: grid` on containers. Let the
content inside stay native.

```css
fieldset {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

label {
  display: flex;
  align-items: center;
  gap: 6px;
}
```

This aligns elements without touching a single visual property.

## Accessibility Comes for Free

Because native elements are used:
- Focus styles are provided by the browser (and respect `prefers-reduced-motion`, high-contrast mode)
- `color-scheme: light dark` means color contrast adapts automatically
- Screen readers already understand `<fieldset>`, `<label>`, `<button>`, `<details>`
- Keyboard navigation works without JavaScript

Avoid overriding `outline` — the browser's focus ring is there for a reason.

## What to Say When Applying This Skill

When designing a new page or component:
1. **Identify the function first** — what does each piece of UI need to do?
2. **Find the native element** that does it — check the MDN element list
3. **Write the HTML** using semantic elements, minimal nesting
4. **Add spacing-only CSS** to lay it out
5. **Stop** — if a property you're about to add is purely visual, ask whether it's necessary

When reviewing existing UI for brutalism compliance, flag:
- Custom font-family, font-size overrides on semantic elements
- color/background-color that isn't using system color keywords
- border-radius (decorative rounding)
- CSS resets (normalize.css, reset.css)
- JavaScript used where a native element would work
