---
name: apple-style-design
description: >-
  Design and build anything in the "Apple style" aesthetic distilled from Dribbble's apple-style tag (64 shots analyzed): iOS/macOS/visionOS-grade UI, Liquid Glass materials, squircle cards, widgets, pill buttons, SF-style typography, soft layered shadows, mesh-gradient backdrops, spring motion. Use this skill whenever the user wants something to look "Apple-like", "iOS style", "macOS style", "clean and premium", "Liquid Glass", "glassmorphism", "like an Apple widget", "minimal but polished", or asks to design or restyle a website, landing page, web app, dashboard, mobile screen, desktop app, plugin panel (Nuke/PySide, ComfyUI), button, toggle, card, icon, widget, poster, slide or product page and wants a premium, calm, high-craft look, even if they never say "Apple".
---

# Apple Style Design

A complete design language reverse-engineered from the Dribbble `apple-style` tag (64 shots, Oct 2026) and cross-checked against Apple's own HIG conventions. It covers tokens, components, materials, motion, layout, copy and per-platform recipes.

The look in one sentence: **calm neutral canvas, one confident accent, content as the hero, soft depth instead of lines, and motion that feels physical.**

## How to use this skill

1. **Identify the output type** (web page, app screen, widget, plugin panel, icon, poster, motion). Pick the matching recipe in `references/layouts.md`.
2. **Pick a mode**: Light (default for marketing, productivity, health), Dark (media, pro tools, finance, gaming, VFX), or Glass-over-image (visionOS, hero sections, players). See "Mode picker" below.
3. **Load tokens**. For web, copy `assets/apple-style.css` into the project (or inline it) and build with its variables and `.as-*` classes. For other platforms read `references/platforms.md` (Qt/PySide QSS for Nuke, ComfyUI frontend, Tailwind, SwiftUI, Figma, slides, Remotion).
4. **Compose with components** from `references/components.md`. Do not invent new styles for a button or list row; the recipes already encode the micro details.
5. **Add materials and motion** last: `references/materials.md` (Liquid Glass, frosted, mesh gradients, grain) and `references/motion.md` (springs, reveals, press states).
6. **Run the QA checklist** at the bottom before showing the result.

Need proof of a pattern or a visual reference? `references/shot-catalog.md` lists every analyzed shot and what it teaches. `assets/demo.html` is a working gallery of every component built with the stylesheet: open it to see the target quality bar.

## The 12 laws (why it looks "Apple")

These are the patterns that showed up across nearly every strong shot. Each has a reason; keep the reason in mind when a case is not covered.

1. **Neutral canvas, colored content.** Backgrounds are off-white `#F5F5F7` / grouped gray `#F2F2F7` or near-black `#000`/`#1C1C1E`. Color is reserved for data, state and one primary action. Reason: the canvas recedes so content and the accent carry all the meaning.
2. **One accent per screen.** System blue `#007AFF` by default; violet `#5E5CE6`, pink, orange or green when the product has its own identity. A second accent only for data series (e.g. orange/pink alternating bars). Reason: a single accent makes the primary action obvious with zero labels.
3. **Depth by elevation, not borders.** Cards float on soft, wide, low-opacity shadows; separators are 0.5px hairlines inset from the left edge. Heavy 1px gray borders read as "web form", not Apple.
4. **Continuous corners everywhere.** Squircle-like radii: 10 (controls), 14 (fields), 20 (list groups, cards), 28 (widgets, sheets), 38+ (device/window), 999 (pills). Nested radius = outer radius minus padding.
5. **Typography does the hierarchy.** SF Pro / Inter, tight negative tracking at display sizes, bold large titles, gray secondary text instead of smaller sizes. Numbers are heroes: `12.203` big and bold with a small gray unit beside it on the same baseline.
6. **Gray is a scale, not a color.** Label opacities: primary 100%, secondary 74% light / 60% dark (Apple ships 60% in light, which is only 3.44:1 on white), tertiary 30%, quaternary 18%. Never invent a random `#999`.
7. **Pills and circles for actions.** Primary buttons are full pills; icon actions are 44px circles; FABs are filled accent circles with a white SF-style glyph and a soft colored shadow.
8. **Materials over flat fills.** Overlays, toolbars, docks, sidebars and players use translucent blurred material (Liquid Glass) so the context shows through.
9. **Generous, rhythmic whitespace.** 4pt grid; 16/20 inner padding; sections breathe (96-160px on desktop). If it feels a bit empty, it is probably right.
10. **Motion is physical.** Springs, not linear tweens. Press = scale 0.97, release = spring back. Reveals fade + rise 8-24px + unblur. Nothing bounces more than once.
11. **Copy is short and confident.** Sentence case, periods on taglines ("Sound. Refined.", "Coming Soon."), two-tone headlines with a gray or accent phrase, lowercase widget titles allowed ("steps walked").
12. **Craft in the micro details.** Chevrons in tertiary gray, tabular numerals for data, keycap hints (`esc`, `return`), status dots, 0.5px hairlines, inner top highlights on glass, colored glow under charts. These details are the difference between "clean" and "Apple".

## Mode picker

| Product feels like | Mode | Canvas | Surface | Accent idea |
|---|---|---|---|---|
| Health, productivity, commerce, docs, SaaS marketing | Light | `#F5F5F7` / `#F2F2F7` | `#FFFFFF` | Blue `#007AFF` |
| Media player, music, finance tickers, pro/VFX tools, gaming | Dark | `#000000` | `#1C1C1E` / `#2C2C2E` | Pink `#FF375F`, green `#30D158`, violet `#5E5CE6` |
| Hero over photo/video, visionOS, players, toggles | Glass | image or mesh gradient | Liquid Glass | White primary, accent secondary |
| Brand/poster/launch | Gradient | mesh gradient + grain | glass or none | Product color |

## Core tokens (summary)

Full tables with dark values and rationale: `references/tokens.md`. Implemented in `assets/apple-style.css`.

- **Font stack**: `-apple-system, BlinkMacSystemFont, "SF Pro Display", "SF Pro Text", "Inter", "Helvetica Neue", Arial, sans-serif`. Load Inter (400/500/600/700) from Google Fonts as the cross-platform fallback. Mono: `"SF Mono", ui-monospace, "JetBrains Mono", Menlo, monospace`.
- **Type scale (app)**: Large Title 34/41 700 (-0.022em) · Title1 28/34 700 · Title2 22/28 700 · Title3 20/25 600 · Headline 17/22 600 · Body 17/22 400 · Callout 16/21 · Subhead 15/20 · Footnote 13/18 · Caption 12/16 · Caption2 11/13.
- **Type scale (marketing)**: Hero 64-96px 700, line-height 1.04, tracking -0.035em · Section 40-56px 600 -0.028em · Lead 21-24px 400 secondary color · Eyebrow 14-17px 600 in accent.
- **Spacing**: 2, 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128, 160.
- **Radius**: 6 (tags), 10 (buttons/controls), 14 (fields), 20 (cards/lists), 28 (widgets/sheets), 38 (windows/devices), 999 (pills).
- **Shadow (light)**: `0 1px 2px rgb(0 0 0/.04), 0 4px 12px rgb(0 0 0/.05), 0 16px 40px rgb(0 0 0/.08)`. Floating: add `0 32px 80px rgb(0 0 0/.12)`.
- **Easing**: standard `cubic-bezier(.25,.1,.25,1)`, emphasized out `cubic-bezier(.32,.72,0,1)`, spring `linear()` curve in `motion.md`. Durations 150 (press), 250 (state), 400 (enter), 600-900 (hero reveals).

## Anti-patterns (seen in the scrape, do not copy)

The tag also contained off-style shots. They teach what to avoid:

- Skeuomorphic 2012 gloss: embossed inputs, beveled "Login" buttons, linen textures (OTAir app store shot).
- Cartoon mascots, sticker outlines and heavy outlines (Taco, Buzz Addiction).
- All-caps monospace "tech brutalist" pages (MEMBRAN): a valid style, but not Apple.
- Neon multi-gradient buttons on every element, and more than one gradient per card.
- Hard black drop shadows offset to one side (the "Astro" device frames use a brutalist offset shadow: wrong for Apple style).
- Default 1px `#ddd` borders on every card, `#999` text, Bootstrap blue `#0d6efd`.
- Bouncy overshoot animations, spinning loaders on everything, parallax that fights scrolling.
- Using Apple's logo or trademarks in the user's product. Use the style, never the brand.

## Output contract

When this skill produces a design:

- Ship working code, not a description. Web: semantic HTML + the token CSS (inline or linked) + minimal JS for motion. Other targets: the platform recipe.
- Always support light and dark unless the mode picker says dark-only, and respect `prefers-reduced-motion`.
- Accessibility is part of the look: 4.5:1 text contrast (`label-2` is tuned to pass on white, canvas and grouped gray; `label-3` is only for placeholders, chevrons and disabled states, never for text people must read), 44x44 touch targets, visible focus ring (3px `accent-text` outline, 2px offset: an outline, never a box-shadow, so component shadows cannot hide it), labels on icon buttons.
- Raw system accents fail contrast as button fills and as small text (white on `#007AFF` = 4.02:1, on `#0A84FF` = 3.65:1). Fill buttons with `accent-fill`, color text with `accent-text`, keep raw `accent` for glows, toggles, icons and big shapes. Safe shades per hue: `references/tokens.md` 3a.
- State the mode, accent and the 2-3 signature details used in one short line after delivering, so the user can steer.

## QA checklist (run before showing)

- [ ] Canvas is neutral; only one accent color drives actions.
- [ ] Accent passes contrast: button fills use `accent-fill`, accent text uses `accent-text` (tokens.md 3a); a custom hue had its ratios computed.
- [ ] No hard borders on cards; separators are hairlines, inset, and lighter at 1x DPR.
- [ ] Radio groups with long labels or hints are single-choice lists with a checkmark, not cramped segmented controls.
- [ ] Compact desktop controls grow to 44px under `pointer: coarse`.
- [ ] Radii follow the scale and nested radii are concentric.
- [ ] Display text has negative tracking; secondary text uses the gray scale, not size.
- [ ] Hero numbers/titles are big; units/labels small and gray on the same baseline.
- [ ] Primary action is a pill (or accent FAB); icon buttons are 44px circles.
- [ ] Overlays/toolbars use material blur with inner highlight, not flat gray.
- [ ] Shadows are soft and layered; nothing looks pasted on.
- [ ] Press, hover, focus states exist; motion uses springs/ease-out; reduced motion respected.
- [ ] Dark mode uses layered grays (`#1C1C1E` / `#2C2C2E` / `#3A3A3C`), not pure black surfaces on black.
- [ ] Copy is short, sentence case, confident; no lorem ipsum in delivered work.
- [ ] Mobile width works with 16-20px gutters and no horizontal scroll.
