# Amber Black Fox

Amber Black Fox is a Firefox profile CSS theme. It uses pure black surfaces, white text, amber accents, and a star GIF background.

![image-20260506001603289](https://raw.githubusercontent.com/Jamir-boop/markdown-images/master/2026-05-06_00-16-03-image-20260506001603289.png)

## Preview

The browser chrome uses `img/background.gif` as toolbar background.

## Requirements

- Firefox desktop.
- Custom profile styles enabled.
- `userChrome.css` and `userContent.css` installed in active Firefox profile.

## Enable Firefox Profile CSS

1. Open `about:config`.
2. Set `toolkit.legacyUserProfileCustomizations.stylesheets` to `true`.
3. Open `about:profiles`.
4. Find active profile root directory.
5. Create `chrome` folder inside profile if missing.

## Installation

Copy these repo files into profile `chrome` folder:

```text
userChrome.css
userContent.css
img/background.gif
```

Expected profile layout:

```text
<profile>/chrome/userChrome.css
<profile>/chrome/userContent.css
<profile>/chrome/img/background.gif
```

Restart Firefox.

## CSS Customizations Included

- Black browser chrome and Firefox panels.
- White toolbar icons.
- Transparent active tabs with amber border.
- Amber hover states at low opacity.
- Amber-black URL bar, search bar, find bar, and selection colors.
- Amber-black native context menu styling where Firefox profile CSS permits it.
- Amber-black `about:*` pages through `userContent.css`.

## Files

- `userChrome.css`: browser UI, tabs, toolbar, URL bar, panels, menus, sidebar.
- `userContent.css`: Firefox content pages, mainly `about:*`.
- `img/background.gif`: toolbar background image.
