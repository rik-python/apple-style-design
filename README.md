# Apple Style Design

A Claude Code skill that makes anything you build look calm, premium and "Apple-like": web pages, dashboards, app screens, widgets, plugin panels (Nuke/PySide, ComfyUI), slides and motion.

It is a full design language distilled from the 64 shots on Dribbble's `apple-style` tag and cross-checked against Apple's Human Interface Guidelines: tokens, components, Liquid Glass materials, spring motion, layout recipes, copy rules and a QA checklist.

**The look in one sentence:** calm neutral canvas, one confident accent, content as the hero, soft depth instead of lines, and motion that feels physical.

## Install

Copy this folder into your Claude Code skills directory:

```bash
git clone https://github.com/rik-python/apple-style-design ~/.claude/skills/apple-style-design
```

Claude picks it up on its own whenever you ask for an Apple-like, iOS, macOS, Liquid Glass or "clean and premium" look, or you can ask for it by name.

## What's inside

| Path | What it is |
|---|---|
| `SKILL.md` | The 12 laws of the style, mode picker (light, dark, glass, gradient), output contract and QA checklist |
| `references/tokens.md` | Colors (light and dark), contrast-safe accent shades, type scale, spacing, radius, elevation, materials, motion |
| `references/components.md` | Buttons, segmented controls, toggles, fields, chips, inset grouped lists, cards, widgets, navigation, overlays, data, media |
| `references/materials.md` | Frosted material, Liquid Glass in CSS, refraction, mesh gradients, grain, glow |
| `references/motion.md` | Spring curves, press states, reveals, number and chart animation, reduced motion |
| `references/layouts.md` | Recipes per output: landing page, dashboard, iOS screens, widgets, desktop apps and plugin panels, visionOS, posters |
| `references/platforms.md` | Qt/PySide QSS for Nuke, ComfyUI frontend, Tailwind, SwiftUI, Figma, slides, Remotion |
| `references/shot-catalog.md` | Every analyzed shot, linked, with what it teaches (and which ones to avoid) |
| `assets/apple-style.css` | Drop-in tokens and `.as-*` component classes, light and dark |
| `assets/demo.html` | Gallery of every component built with the stylesheet |
| `evals/` | Test prompts and graders used to check the skill against a no-skill baseline |

## See the demo

Serve the `assets` folder and open the gallery:

```bash
python -m http.server 3200 --directory assets
```

Then visit `http://127.0.0.1:3200/demo.html`.

## Accessibility built in

The raw system accents fail contrast as button fills (white on `#007AFF` is 4.02:1). The stylesheet ships an AA-safe `fill` and `text` shade for every hue, focus rings, 44px touch targets on touch screens, hairlines tuned for 1x displays and `prefers-reduced-motion` support.

## Not affiliated with Apple

This is an independent style study. It uses no Apple logos, icons, fonts or other assets, and it tells Claude never to put Apple's brand in your product. "Apple" is used only to describe the visual style. Shots referenced in the catalog belong to their creators on Dribbble and are linked, not copied.

## License

MIT, see `LICENSE`.
