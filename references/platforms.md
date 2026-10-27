# Platform recipes

How to apply the tokens outside plain HTML/CSS. Values come from `tokens.md`.

## Contents
1. Web: plain CSS (default)
2. Tailwind CSS
3. React / Next.js
4. SwiftUI (native Apple)
5. Qt / PySide (Nuke, Houdini, Maya, standalone tools)
6. ComfyUI frontend extensions
7. Figma
8. Remotion / motion video
9. Slides (pptx / Google Slides)

---

## 1. Web: plain CSS

Copy `assets/apple-style.css` into the project. It contains tokens, light/dark switching (`prefers-color-scheme` plus `[data-theme]` override), base typography and all `.as-*` component classes. `assets/demo.html` shows each class in use: read it to copy markup patterns rather than rewriting them.

Font loading:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
```
Apple devices will use SF through `-apple-system`; everyone else gets Inter with the optical size axis.

## 2. Tailwind CSS

```js
// tailwind.config.js (v3) or translate to @theme in v4
theme: { extend: {
  colors: {
    canvas: 'var(--as-bg-canvas)', grouped: 'var(--as-bg-grouped)', surface: 'var(--as-surface)',
    'surface-2': 'var(--as-surface-2)', 'surface-3': 'var(--as-surface-3)',
    label: 'var(--as-label)', 'label-2': 'var(--as-label-2)', 'label-3': 'var(--as-label-3)',
    accent: 'var(--as-accent)', separator: 'var(--as-separator)',
  },
  fontFamily: { sans: ['-apple-system','BlinkMacSystemFont','"SF Pro Text"','Inter','"Helvetica Neue"','Arial','sans-serif'] },
  borderRadius: { xs: '6px', sm: '10px', md: '14px', lg: '20px', xl: '28px', '2xl': '38px' },
  boxShadow: {
    e1: '0 1px 2px rgb(0 0 0/.04), 0 2px 8px rgb(0 0 0/.04)',
    e2: '0 1px 2px rgb(0 0 0/.04), 0 4px 12px rgb(0 0 0/.05), 0 16px 40px rgb(0 0 0/.08)',
    e3: '0 1px 2px rgb(0 0 0/.04), 0 4px 12px rgb(0 0 0/.05), 0 16px 40px rgb(0 0 0/.08), 0 32px 80px rgb(0 0 0/.12)',
  },
  letterSpacing: { display: '-0.035em', title: '-0.022em', body: '-0.01em' },
  transitionTimingFunction: { 'ios-out': 'cubic-bezier(.32,.72,0,1)' },
}}
```
Keep the CSS variables from `apple-style.css` loaded so dark mode works through the vars. Glass needs custom classes (`backdrop-blur-xl backdrop-saturate-[1.8]` plus the inset highlight shadow).

shadcn/ui: set `--radius: 0.875rem`, map `--primary` to the accent, `--muted` to `surface-2`, `--border` to the separator, and replace default `border` on cards with `shadow-e1 border-0`.

## 3. React / Next.js

- Use Framer Motion (`motion`) with the springs in `motion.md`. `whileTap={{ scale: .97 }}` on buttons, `layout` + `layoutId` for segmented thumbs and shared elements.
- Use `next/font/google` for Inter with `axes: ['opsz']`.
- Icons: `lucide-react` with `strokeWidth={1.75}` at 20px.

## 4. SwiftUI

If the target is a real Apple app, do not imitate: use system components and they will already look right. `.background(.regularMaterial)`, iOS 26 `.glassEffect()`, `List { }.listStyle(.insetGrouped)`, `.font(.largeTitle.bold())`, `.buttonStyle(.borderedProminent)` with `.buttonBorderShape(.capsule)`, `.contentTransition(.numericText())` for counters, `.symbolEffect(.bounce)` for icons.

## 5. Qt / PySide (Nuke panels, DCC tools)

Nuke and most DCCs run PySide2/6. QSS cannot blur, so use the "dark macOS inspector" variant: layered grays, hairlines, pills, one accent.

```python
APPLE_DARK_QSS = """
* { font-family: "SF Pro Text", "Inter", "Segoe UI", sans-serif; font-size: 13px; color: #FFFFFF; }
QWidget { background: #1C1C1E; }
QFrame#card { background: #2C2C2E; border-radius: 10px; }
QLabel[role="section"] { color: rgba(235,235,245,0.3); font-size: 11px; font-weight: 600; text-transform: uppercase; }
QLabel[role="secondary"] { color: rgba(235,235,245,0.6); }
QPushButton { background: rgba(118,118,128,0.24); border: none; border-radius: 14px; padding: 6px 14px; min-height: 16px; }
QPushButton:hover { background: rgba(118,118,128,0.32); }
QPushButton:pressed { background: rgba(118,118,128,0.44); }
QPushButton[primary="true"] { background: #0A84FF; font-weight: 600; }
QPushButton[primary="true"]:hover { background: #2B95FF; }
QLineEdit, QSpinBox, QDoubleSpinBox, QComboBox { background: rgba(118,118,128,0.24); border: 1px solid transparent; border-radius: 7px; padding: 4px 8px; selection-background-color: #0A84FF; }
QLineEdit:focus, QSpinBox:focus, QDoubleSpinBox:focus, QComboBox:focus { border: 1px solid rgba(10,132,255,0.8); }
QSlider::groove:horizontal { height: 4px; background: rgba(120,120,128,0.36); border-radius: 2px; }
QSlider::sub-page:horizontal { background: #0A84FF; border-radius: 2px; }
QSlider::handle:horizontal { background: #FFFFFF; width: 18px; height: 18px; margin: -7px 0; border-radius: 9px; }
QCheckBox::indicator { width: 18px; height: 18px; border-radius: 9px; border: 1.5px solid rgba(235,235,245,0.3); }
QCheckBox::indicator:checked { background: #0A84FF; border-color: #0A84FF; }
QTabBar::tab { background: transparent; color: rgba(235,235,245,0.6); padding: 6px 12px; border-radius: 7px; }
QTabBar::tab:selected { background: #636366; color: #FFFFFF; }
QScrollBar:vertical { background: transparent; width: 8px; }
QScrollBar::handle:vertical { background: rgba(235,235,245,0.2); border-radius: 4px; min-height: 24px; }
QScrollBar::add-line, QScrollBar::sub-line { height: 0; }
QToolTip { background: #3A3A3C; color: #FFFFFF; border: none; border-radius: 6px; padding: 4px 8px; }
"""
# widget.setStyleSheet(APPLE_DARK_QSS); btn.setProperty("primary", True)
```

Use `QGraphicsDropShadowEffect(blurRadius=40, offset=(0,12), color=QColor(0,0,0,110))` for floating panels. Animate with `QPropertyAnimation` + `QEasingCurve.OutCubic` (220ms). Toggle switch: subclass `QAbstractButton`, paint a 34x20 rounded track and 16px knob, animate a `knobX` property with `OutBack`.

## 6. ComfyUI frontend extensions

ComfyUI's Vue frontend exposes CSS variables (`--comfy-menu-bg`, `--comfy-input-bg`, `--input-text`, `--border-color`, `--fg-color`, `--bg-color`). For custom sidebar tabs, dialogs and DOM widgets:

- Scope styles under your extension root class to avoid restyling the whole app.
- Use the dark token set; set `background: rgb(28 28 30 / .82); backdrop-filter: blur(24px) saturate(180%)` for floating panels over the canvas (canvas content behind makes glass work).
- Radius 10-14 for panels, 7 for inputs; 13px type; one accent for the primary action; keycap hints for shortcuts.
- Node colors stay as the user sets them; only restyle your own UI.

## 7. Figma

Create variables collections: `color` (light/dark modes using the tables in tokens.md), `radius`, `space`. Text styles named after the iOS scale (Large Title ... Caption 2) with tracking in %, e.g. -2.2% for 34px. Effect styles e1/e2/e3 and "Glass" (background blur 30 + inner shadows). Use Apple's official iOS/macOS UI kits as the base when available.

## 8. Remotion / motion video

- 1920x1080 or 1080x1920, 30/60fps. Backgrounds: mesh gradient + grain, or pure black for product reveals.
- Use `spring()` configs from `motion.md`. Text reveals: word stagger 3-4 frames, blur 8 -> 0 via `interpolate`.
- Product reveal: rim light sweep over a dark product, slow 2-3% scale push, tagline in two beats.
- Audio: soft clicks and whooshes, low and short; music minimal.

## 9. Slides

Black or white masters; Inter/SF only; one idea per slide; titles 40-60pt 600 with -2% tracking; big-number slides; images full-bleed or inside radius-28 cards; no bullet walls (max 3 short lines).
