# Amber Black Theme Style Guide

Use this guide when building custom themes for tools, websites, apps, editors, file managers, terminals, or other software.

Goal: high contrast monochrome amber theme. Pure black base. Full amber interaction states. Text is mostly white or black, not yellow.

## Core Rules

- Background must be pure black: `#000000` or `rgb(0, 0, 0)`.
- Main accent must be amber: `#FFB900` or `rgb(255, 185, 0)`.
- Text must be white on black surfaces.
- Text must be black on amber surfaces.
- Use yellow text only for small metadata, accents, code tokens, or low-risk decorative emphasis.
- No blue, green, red, purple, pink, brown, beige, slate, or gradient palettes.
- Do not use soft colorful tints from other hues.
- Do not use decorative gradients, orbs, bokeh, or theme art.
- Keep UI sharp, dense, practical, and high contrast.
- Do not use muddy transparent amber. Prefer solid `#FFB900` or amber-brown borders.
- Use amber alpha only when unavoidable: alpha `0.04` or lower, or alpha `0.92` or higher.
- Reject amber alpha from `0.05` through `0.91`, including comma-rgba amber at alpha `.10` and `.55`.

## Palette

Use these exact tokens when possible.

```css
:root {
  --bg: #000000;
  --surface-0: #000000;
  --surface-1: #050505;
  --surface-2: #080808;
  --surface-3: #101010;

  --text: #FFFFFF;
  --text-muted: #A0A0A0;
  --text-disabled: #555555;
  --text-on-accent: #000000;

  --accent: #FFB900;
  --accent-hover: #FFB900;
  --accent-active: #FFB900;
  --accent-outline: #FFB900;

  --border: #332500;
  --border-strong: #664A00;
}
```

JSON theme mapping:

```json
{
  "Background": "000000",
  "Surface": "080808",
  "Foreground": "101010",
  "Text": "FFFFFF",
  "Secondary": "A0A0A0",
  "Border": "332500",
  "Outline": "664A00",
  "Selection": "FFB900",
  "Hover": "FFB900",
  "ContentHover": "000000",
  "ContentSelection": "000000",
  "IconTint": "FFB900",
  "Disabled": "555555"
}
```

## Component Rules

Base surfaces:
- Main window, document, sidebar, panels, dialogs, popovers, menus, toolbars, tabs, inputs, and code blocks use black or near-black.
- Borders use amber-brown dark values. Use borders before transparent amber fills.
- Separators must be subtle, not gray-heavy.

Text:
- Normal text: white.
- Secondary text: neutral gray.
- Disabled text: dark gray.
- Text on selected or hovered amber rows: black.

Hover and selection:
- Full-row hover should be solid amber.
- Full-row selected state should be solid amber.
- Hover text and selected text must be black.
- Focus ring should be solid amber outline, not blue.
- Do not use middle-alpha amber for hover, active, selected, or focus states.

Icons and SVG:
- Icons should inherit `currentColor`.
- On black surfaces, icon color should be amber or white.
- On amber hover/selection, icon color must be black.
- Force SVG fill and stroke when needed.

```css
.menu-item:hover,
.row:hover,
.button:hover {
  background: var(--accent) !important;
  color: var(--text-on-accent) !important;
}

.menu-item:hover *,
.row:hover *,
.button:hover * {
  color: currentColor !important;
  -webkit-text-fill-color: currentColor !important;
}

.menu-item:hover svg,
.menu-item:hover svg *,
.row:hover svg,
.row:hover svg * {
  fill: currentColor !important;
  stroke: currentColor !important;
}
```

Context menus:
- Menu background black.
- Menu row hover amber.
- Menu text on hover black.
- Menu and menu rows must use square corners.
- Submenu carets, shortcut text, icon fonts, and inline SVGs must stay visible.
- Firefox submenu arrows use `menupopup > menu::after`; old `.menu-right` may not apply.
- Do not use broad active-menu descendant rules like `menupopup > menu[_moz-menuactive] *`; that can recolor nested submenu contents.
- Button groups inside menu rows should stay transparent on row hover.
- Individual buttons inside menu rows may use subtle black overlay on hover.

```css
.context-menu,
.context-menu *,
menupopup,
menupopup::part(content),
menupopup > menu,
menupopup > menuitem {
  border-radius: 0 !important;
}

.context-menu li:hover {
  background: var(--accent) !important;
  color: var(--text-on-accent) !important;
}

.context-menu li:hover a,
.context-menu li:hover span,
.context-menu li:hover i,
.context-menu li:hover .fa,
.context-menu li:hover .ty-icon,
.context-menu li:hover .fa::before,
.context-menu li:hover .ty-icon::before,
.context-menu li:hover .ty-icon::after {
  color: var(--text-on-accent) !important;
  -webkit-text-fill-color: currentColor !important;
}

.context-menu li:hover svg,
.context-menu li:hover svg * {
  fill: currentColor !important;
  stroke: currentColor !important;
}

.context-menu li.has-btn-submenu:hover .menu-style-btn {
  background: transparent !important;
  color: var(--text-on-accent) !important;
  opacity: 1 !important;
}

.context-menu li.has-btn-submenu:hover .menu-style-btn:hover {
  background: rgba(0, 0, 0, 0.16) !important;
}

.context-menu li.has-btn-submenu:hover .menu-style-btn.disabled {
  color: rgba(0, 0, 0, 0.45) !important;
  opacity: 1 !important;
}
```

Firefox submenu arrows:

```css
menupopup > menu::after {
  fill: #FFFFFF !important;
  fill-opacity: 1 !important;
  -moz-context-properties: fill, fill-opacity !important;
}

menupopup > menu[_moz-menuactive="true"]:not([disabled="true"])::after {
  fill: #000000 !important;
  fill-opacity: 1 !important;
}

menupopup > menu[_moz-menuactive="true"]:not([disabled="true"]) > :is(
  .menu-text,
  .menu-accel,
  .menu-icon,
  .menu-highlightable-text
) {
  color: #000000 !important;
  fill: #000000 !important;
  stroke: #000000 !important;
}
```

Firefox URL options:
- URL dropdown/options must not have row borders, box-shadow, or outline.
- URL hover and selected states must use solid amber with black text and icons.
- URL input itself can keep black background and amber focus border/outline.

```css
.urlbarView-row,
.searchbar-engine-one-off-item {
  border: 0 !important;
  box-shadow: none !important;
  outline: none !important;
}

.urlbarView-row:hover,
.urlbarView-row[selected],
.urlbarView-row[aria-selected="true"],
.searchbar-engine-one-off-item:hover,
.searchbar-engine-one-off-item[selected] {
  background: var(--accent) !important;
  color: var(--text-on-accent) !important;
}
```

Firefox autoscroll:
- Middle-click autoscroll indicator uses `#autoscroller` and/or `.autoscroller`.
- If the default icon is black on black, give the autoscroller solid amber background and black border.
- Direction variants can use `[scrolldir="NS"]` and `[scrolldir="EW"]`.

Inputs and buttons:
- Inputs black, white text, amber border.
- Focus uses amber ring.
- Primary buttons solid amber with black text.
- Secondary buttons black with amber border.

```css
input,
select,
textarea,
button {
  background: var(--bg);
  color: var(--text);
  border: 1px solid var(--border);
}

input:focus,
select:focus,
textarea:focus,
button:focus {
  outline: 2px solid var(--accent-outline);
  outline-offset: 2px;
}

.primary {
  background: var(--accent);
  color: var(--text-on-accent);
  border-color: var(--accent);
}
```

Tables and lists:
- Headers use black or near-black with amber-brown border.
- Alternate rows use near-black.
- Row hover uses solid amber only if app pattern supports full-row selection; otherwise use border or near-black.
- List markers can be amber.

Code:
- Code blocks should be black with amber border.
- Inline code should use black or near-black background with amber border.
- Prefer Caskaydia/Cascadia code fonts with ligatures.
- Keep normal prose font separate from code font.

```css
:root {
  --code-font: "CaskaydiaCove NF", "CaskaydiaCove NFM", "Cascadia Code NF",
    "Cascadia Code", monospace;
}

code,
pre,
.code,
.CodeMirror {
  font-family: var(--code-font);
  font-variant-ligatures: contextual common-ligatures;
  font-feature-settings: "calt" 1, "liga" 1;
  text-rendering: optimizeLegibility;
}
```

Syntax highlighting:
- Use amber brightness levels and white, not full rainbow.
- Keywords: bright amber.
- Strings: pale amber.
- Numbers: accent amber.
- Comments: muted gray or muted amber-brown.
- Errors: amber underline or amber border, not red.

Print and export:
- Export should keep black background unless user requests paper-friendly mode.
- If export remains dark, set print color adjustment exact.

```css
@media print {
  * {
    print-color-adjust: exact;
    -webkit-print-color-adjust: exact;
  }

  body {
    background: #000000;
    color: #FFFFFF;
  }
}
```

## Accessibility

- Minimum text contrast target: WCAG AA.
- White on black is default for content.
- Black on amber is default for hover, active, selected, and primary action.
- Do not place amber text on amber background.
- Do not place gray text on black for primary content.
- Disabled controls must remain visible.
- Icons must not disappear on hover.

## Agent Workflow

1. Inspect existing theme first.
2. Identify all color variables and hardcoded color values.
3. Replace color system with black, white, gray, and amber only.
4. Prefer official app theme tokens before broad selectors.
5. Add targeted selectors for UI parts missed by tokens.
6. Keep layout, fonts, spacing, and animations unchanged unless user asks.
7. Add hover/selection/icon inheritance rules for menus and rows.
8. Validate color scan after edits.
9. Reject middle-alpha amber. Use borders or solid amber instead.

Color scan should allow only:
- black
- white
- neutral gray
- amber `255, 185, 0`
- amber-derived values
- transparent

Reject these:
- blue progress or selection
- red warning
- green success
- purple syntax token
- colorful match highlights
- white export mode unless user asks
- comma-rgba amber at alpha `.10`
- comma-rgba amber at alpha `.55`
- any `#FFB900` alpha where alpha is `0.05` through `0.91`

## Final Verification

Check these UI states:
- app background
- sidebar
- active item
- hover row
- selected row
- context menu
- context menu square corners
- submenu icons
- button group icons
- URL dropdown/options with no borders
- inputs and focus
- code blocks
- inline code
- syntax highlighting
- search matches
- disabled controls
- print/export

Stop only when UI reads as: pure black base, amber interaction, black/white text, no stray hue.
