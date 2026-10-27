# Tokens

Canonical values for every platform. `assets/apple-style.css` implements these as CSS custom properties with the same names (prefix `--as-`).

## Contents
1. Color: neutrals (light/dark)
2. Color: labels and fills
3. Color: system accents
4. Color: measured from the shots
5. Typography
6. Spacing and layout
7. Radius
8. Elevation (shadows)
9. Materials
10. Motion
11. Z-index and sizes

---

## 1. Neutrals

| Token | Light | Dark | Use |
|---|---|---|---|
| `bg` | `#FFFFFF` | `#000000` | Plain page background |
| `bg-grouped` | `#F2F2F7` | `#000000` | Behind inset grouped lists (iOS Settings look) |
| `bg-canvas` | `#F5F5F7` | `#0B0B0C` | Marketing canvas, stage behind widgets |
| `surface` | `#FFFFFF` | `#1C1C1E` | Cards, list groups, sheets |
| `surface-2` | `#F2F2F7` | `#2C2C2E` | Nested cards, fields, segmented track |
| `surface-3` | `#E5E5EA` | `#3A3A3C` | Pressed rows, chips, keycaps |
| `separator` | `rgba(60,60,67,.29)` | `rgba(84,84,88,.6)` | 0.5px hairlines |
| `separator-opaque` | `#C6C6C8` | `#38383A` | When hairline sits on images |

Hairlines on 1x screens: line widths snap to whole device pixels, so a `0.5px` separator draws as a full 1px at 1x-1.25x DPR (100-125% Windows/Linux displays) and looks twice as heavy as on Retina. Keep `0.5px` in the code and lower the alpha there instead: `@media (max-resolution: 1.49dppx)` with `rgba(60,60,67,.18)` light and `rgba(84,84,88,.4)` dark. The stylesheet already does this.

Rule: dark mode never puts `#000` cards on `#000` canvas. Step up through `#1C1C1E` -> `#2C2C2E` -> `#3A3A3C` for each elevation level. The event-discovery shot uses `#16181D` canvas and `#202127` cards: same idea, slightly blue-tinted, which suits media apps.

## 2. Labels and fills

| Token | Light | Dark |
|---|---|---|
| `label` | `#000000` (or `#1D1D1F` on marketing) | `#FFFFFF` |
| `label-2` (secondary) | `rgba(60,60,67,.74)` (Apple: .60) | `rgba(235,235,245,.60)` |
| `label-3` (tertiary) | `rgba(60,60,67,.30)` | `rgba(235,235,245,.30)` |
| `label-4` (quaternary) | `rgba(60,60,67,.18)` | `rgba(235,235,245,.16)` |
| `fill` | `rgba(120,120,128,.20)` | `rgba(120,120,128,.36)` |
| `fill-2` | `rgba(120,120,128,.16)` | `rgba(120,120,128,.32)` |
| `fill-3` | `rgba(118,118,128,.12)` | `rgba(118,118,128,.24)` |
| `fill-4` | `rgba(116,116,128,.08)` | `rgba(118,118,128,.18)` |

Fills are for control backgrounds (search field, chart tracks, toggle off-state, segmented control track). Chart bar tracks in the steps widget are exactly a `fill-4` style light gray capsule.

## 3. System accents

| Name | Light | Dark | Typical role |
|---|---|---|---|
| blue | `#007AFF` | `#0A84FF` | Default primary action, links, FAB |
| indigo | `#5856D6` | `#5E5CE6` | Sleep, focus, AI, premium |
| purple | `#AF52DE` | `#BF5AF2` | Creative, music |
| pink | `#FF2D55` | `#FF375F` | Music, love, heart, play button |
| red | `#FF3B30` | `#FF453A` | Destructive, badge count, end call |
| orange | `#FF9500` | `#FF9F0A` | Activity, warning, energy |
| yellow | `#FFCC00` | `#FFD60A` | Highlights, notes, light theme toggle |
| green | `#34C759` | `#30D158` | Success, toggles on, stock up, call |
| mint | `#00C7BE` | `#63E6E2` | Health secondary |
| teal | `#30B0C7` | `#40C8E0` | Travel, water |
| cyan | `#32ADE6` | `#64D2FF` | Info, weather |
| gray | `#8E8E93` | `#8E8E93` | Chevrons, inactive icons |

Tint recipe for status pills and chips: background = accent at 12-15% alpha, text = the hue's `-text` shade from 3a, optional 6px dot in full accent.

### 3a. Contrast-safe accent shades (check before you pick)

The system hues are tuned for shapes, not for text. Measured WCAG ratios:

- White on `#007AFF` = **4.02:1**, white on `#0A84FF` = **3.65:1**. Both fail 4.5:1 for button labels under 19px bold. Same for pink `#FF375F` (3.52), purple `#BF5AF2` (3.52), green (2.0-2.2), orange (2.1).
- Accent as small text on dark gray fails too: `#5E5CE6` on `#1C1C1E` = 3.36, on `#2C2C2E` = 2.75; `#0A84FF` on `#2C2C2E` = 3.82.

So every accent comes in three roles. `assets/apple-style.css` ships them as `--as-<hue>-fill` / `--as-<hue>-text` and wires `--as-accent-fill` / `--as-accent-text`:

| Hue | `accent` (glow, toggle, icon, big shape) | `fill` (under white text) | `text` light, on `#FFF` / `#F2F2F7` | `text` dark, on `#1C1C1E` / `#2C2C2E` |
|---|---|---|---|---|
| blue | `#007AFF` / `#0A84FF` | `#0071E3` (4.70) | `#0066CC` (5.57 / 4.99) | `#409CFF` (6.01 / 4.92) |
| indigo | `#5856D6` / `#5E5CE6` | light `#5856D6` (5.65), dark `#5E5CE6` (5.06) | `#5856D6` (5.65 / 5.06) | `#8E8CFF` (5.95 / 4.87) |
| pink | `#FF2D55` / `#FF375F` | `#D30F45` (5.35) | `#D30F45` (5.35 / 4.80) | `#FF6482` (5.99 / 4.91) |
| purple | `#AF52DE` / `#BF5AF2` | `#8944AB` (6.04) | `#8944AB` (6.04 / 5.41) | `#DA8FFF` (7.58 / 6.21) |
| green | `#34C759` / `#30D158` | `#1F7A35` (5.39), or keep the vivid fill with black text (9.5+) | `#1F7A35` (5.39 / 4.83) | `#30D158` (8.42 / 6.89) |
| orange | `#FF9500` / `#FF9F0A` | `#C93400` (5.28), or vivid fill with black text (9.5+) | `#C93400` (5.28 / 4.73) | `#FF9F0A` (8.28 / 6.78) |
| red | `#FF3B30` / `#FF453A` | `#C4001A` (6.25) | `#C4001A` (6.25 / 5.60) | `#FF6961` (6.03 / 4.94) |

Rules:
- Changing the accent means changing all three: `--as-accent`, `--as-accent-fill`, `--as-accent-text`. Setting only `--as-accent` on `:root` leaves fill and text on blue. Point all three at the per-hue tokens so dark mode swaps them for you.
- Black text on a vivid fill (`--as-on-accent: #000`) is the Apple-faithful way to keep bright green, orange or yellow buttons.
- Ratios above use the WCAG 2.x relative-luminance formula. For a hue not in this table, compute it before shipping (a ten-line Node or Python snippet does it).

## 4. Measured from the shots

Sampled pixels (median-cut palettes) from the analyzed Dribbble shots:

| Shot | Values | Lesson |
|---|---|---|
| Steps widget | canvas `#F5F6F5`, bars `#FC7616` orange + `#F34FA4` pink, track ~`#EFEFEF` | Two warm hues alternate; track is barely visible |
| Sleep widget | `#5523EE` electric violet surface, white capsule bars, white 60% labels | Full-bleed accent widget, monochrome content on it |
| Flight log | primary blue `#0079FE`, grouped bg `#F2F2F7`, white groups | Pure iOS: inset grouped list + blue FAB |
| Event discovery (dark) | canvas `#16181D`, cards `#202127`, accent `#7968DE` | Blue-black neutrals with soft violet accent |
| Direct messaging | canvas `#E4DFEA` lavender-gray, outgoing bubble `#242FF1` | Saturated cobalt bubbles on airy lavender |
| Quick search modal | glass `#434447` to `#494949` at ~90%, text white | Dark material over a light dashboard |
| Stock widget | `#131313` card, line `#30D158` with green glow fill | Black card + neon data + gradient under line |
| Theme switcher | stage `#BBBFC7` to `#DFE4E2` cool grays, yellow glow `#F5C518` | Glass knob, glowing state color |
| Settings icons | green `#34C759` -> `#8DE29C` highlight; graphite `#646C6A` | App icon: base color + lighter rim highlight |
| Accountant app | stage `#8D9DEE` periwinkle, cards `#070707`, gradient `#3EC5F5` -> `#8B6CF6` | Cyan-to-violet gradient for primary CTA only |
| Coming soon card | lilac `#BBA8D4` / `#CFB9EB` / `#E3D5F0` on `#453645` | Monochrome product-color stage |
| NeoCRM table | `#FFFFFF` / `#F5F5F7`, primary `#1E3FA8` deep blue | Status pills with tinted backgrounds |

## 5. Typography

**Families**
- UI/text: `-apple-system, BlinkMacSystemFont, "SF Pro Text", "Inter", "Helvetica Neue", Arial, sans-serif`
- Display (>= 20px): `-apple-system, BlinkMacSystemFont, "SF Pro Display", "Inter", ...`
- Rounded (widgets, playful numbers): `ui-rounded, "SF Pro Rounded", "Nunito", "Inter", sans-serif`
- Mono: `ui-monospace, "SF Mono", "JetBrains Mono", Menlo, Consolas, monospace`
- Shots that were not on SF used Inter, Plus Jakarta Sans, Manrope or Montserrat. Inter is the closest match; Plus Jakarta Sans works for slightly friendlier marketing pages.

**Tracking** (SF optical tracking approximated for Inter):

| Size | Tracking |
|---|---|
| 11-13px | +0.01em |
| 15-17px | -0.01em |
| 20-28px | -0.018em |
| 34-48px | -0.024em |
| 56-96px | -0.035em |
| 100px+ | -0.045em |

**Weights**: 400 body, 500 for UI labels in dense dashboards, 600 headlines/buttons, 700 large titles and hero numbers. Avoid 300 and 800+ except for a deliberate thin hero number.

**Numerals**: `font-variant-numeric: tabular-nums` for tables, timers, prices, charts. Hero numbers can stay proportional.

**Two-tone headlines**: Main phrase in `label`, a supporting phrase in `label-2` gray or the accent ("So, do you want to make **easier** [gray] the way you **drink water** [blue]?"). Use once per page.

**Gradient text reveal**: hero words fade from `label` to accent to transparent ("Ready for a Whole..." shot). Implement with `background-clip:text` and animate the gradient position.

**Line length**: 45-75 characters for body; hero headlines max ~14 words over 2 lines, balanced (`text-wrap: balance`).

## 6. Spacing and layout

- Base unit 4. Scale: 2, 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128, 160.
- iOS screen gutters 16 (compact) / 20 (regular). List group inset 16-20. Row height min 44, typical 52-60 with subtitle.
- Card padding 16 (dense) / 20 (default) / 24-28 (widgets, feature cards).
- Desktop content max width 980-1200 for marketing text blocks, 1440 for dashboards. Section vertical padding 96-160.
- Bento grid gap 16-20; card aspect ratios 1:1, 2:1, 1:2 mixed.
- Headline to sub-copy 16-24; sub-copy to CTA row 32-40; CTA gap 12-16.

## 7. Radius

| Token | px | Use |
|---|---|---|
| `r-xs` | 6 | Tags, keycaps, small badges |
| `r-sm` | 10 | Buttons (non-pill), segmented items, menu items |
| `r-md` | 14 | Text fields, search fields, small cards |
| `r-lg` | 20 | Cards, inset list groups, modals on web |
| `r-xl` | 28 | Widgets, sheets, feature cards, command palette |
| `r-2xl` | 38 | Windows, device screens, hero media |
| `r-pill` | 999 | Pills, capsules, avatars, chart bars |

Concentric rule: inner radius = outer radius - padding (min 6). A 28px widget with 16px padding gets 12px inner tiles.

Squircle: browsers that support `corner-shape: squircle` get true continuous corners (multiply radius by ~1.6 when using it). Others fall back to the normal radius, which is fine.

## 8. Elevation

| Level | Light | Dark |
|---|---|---|
| e0 flat | none | none |
| e1 resting card | `0 1px 2px rgb(0 0 0/.04), 0 2px 8px rgb(0 0 0/.04)` | `0 0 0 .5px rgb(255 255 255/.08)` |
| e2 raised card / widget | `0 1px 2px rgb(0 0 0/.04), 0 4px 12px rgb(0 0 0/.05), 0 16px 40px rgb(0 0 0/.08)` | `0 0 0 .5px rgb(255 255 255/.08), 0 16px 40px rgb(0 0 0/.5)` |
| e3 floating (popover, FAB, dock) | e2 + `0 32px 80px rgb(0 0 0/.12)` | e2 + `0 32px 80px rgb(0 0 0/.6)` |
| colored glow (FAB, toggle on, chart) | `0 8px 24px color-mix(in srgb, var(--accent) 40%, transparent)` | same at 50% |

Dark mode substitutes shadows with a 0.5px light inner ring, because shadows vanish on black.

## 9. Materials

| Material | Light | Dark | Blur |
|---|---|---|---|
| ultra-thin | `rgb(255 255 255/.35)` | `rgb(30 30 30/.35)` | 20px |
| thin | `rgb(255 255 255/.55)` | `rgb(30 30 30/.55)` | 24px |
| regular | `rgb(250 250 252/.72)` | `rgb(40 40 42/.72)` | 30px |
| thick | `rgb(246 246 248/.86)` | `rgb(44 44 46/.86)` | 40px |

All materials: `backdrop-filter: blur(X) saturate(180%)`. Liquid Glass adds edge highlights and refraction: see `materials.md`.

## 10. Motion

| Token | Value | Use |
|---|---|---|
| `dur-1` | 120ms | Press down, hover tint |
| `dur-2` | 220ms | Toggle, checkbox, segmented slide |
| `dur-3` | 400ms | Enter/exit sheets, popovers |
| `dur-4` | 700ms | Hero reveals, page sections |
| `ease-standard` | `cubic-bezier(.25,.1,.25,1)` | Generic |
| `ease-out` | `cubic-bezier(.32,.72,0,1)` | Sheets, drawers, iOS feel |
| `ease-in-out` | `cubic-bezier(.65,0,.35,1)` | Morphs, crossfades |
| `spring` | see `motion.md` (`linear()` curve) | Press release, toggles, knobs |

## 11. Sizes and z-index

- Touch target min 44x44. Icon button 36 (dense desktop) / 44 (default). FAB 56. Avatar 28/36/44/64.
- Dense desktop vs 44px: they do not conflict. Draw compact controls (28-36px) for mouse users and grow them only on touch with `@media (pointer: coarse)`, or keep the visual size and widen the hit area with a transparent `::before { inset: -4px }` on a positioned element. Never ship a sub-44px control to a coarse pointer. The stylesheet does this for small buttons, chips, search, segmented labels, the toggle (45px tap area) and the round checkbox (44px).
- Icons: SF Symbols look, 1.5px stroke at 20px, round caps and joins. Lucide or Phosphor (regular) are the closest open sets.
- Toggle 51x31 knob 27. Segmented control height 32 (iOS) / 28 (macOS). Text field 44 (iOS) / 32 (macOS dense).
- Z-index: base 0, sticky 10, dropdown 100, overlay 1000, modal 1100, toast 1200.
