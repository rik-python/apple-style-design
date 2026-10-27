# Components

Recipes for every component seen in the analyzed shots. CSS class names match `assets/apple-style.css`. Values reference tokens in `tokens.md`.

## Contents
1. Buttons (pill, secondary, ghost, icon, FAB, store badge)
2. Segmented control and tabs
3. Toggle, checkbox, slider
4. Text field, search field, command palette
5. Chips, tags, status pills, badges, keycaps
6. Lists (inset grouped), rows, disclosure
7. Cards, widgets, bento tiles
8. Navigation: nav bar, large title, sidebar, tab bar, floating dock, window chrome
9. Sheets, modals, popovers, toasts, notifications
10. Data: stat, bar chart, line chart, ring, progress
11. Media: player bar, album tile, avatar, device frame
12. App icons and logo marks

---

## 1. Buttons

**Primary pill** `.as-btn.as-btn--primary`
- Height 44 (default), 36 (small), 52 (hero). Padding-x 20/16/28. Radius pill.
- Fill `accent-fill` (not raw `accent`: white on `#007AFF` is only 4.02:1, see tokens.md 3a), text white 600 at 15-17px, tracking -0.01em.
- Hover: brightness 1.06. Press: `scale(.97)` 120ms, release spring. Focus: `0 0 0 4px` accent 35%.
- Disabled: 40% opacity, no shadow.

**On dark or photo backgrounds** the primary flips: white fill, black text ("Learn more", "Explore", "Buy now" in the shots). The secondary becomes an outline pill: 1px `rgb(255 255 255/.5)` border, white text, transparent or ultra-thin glass fill ("Notify me", "Test Drive").

**Secondary** `.as-btn--secondary`: fill `fill-3` (light gray tint), text accent or label. Used for "Mix", "Skip", "Edit".

**Tinted** `.as-btn--tinted`: accent at 15% fill, accent text. Good for "Add Data", "Edit" capsules (Accountant shot used a tiny blue "Edit" capsule).

**Ghost / text link**: accent text 17px, no fill, chevron optional. "See All", "Read More", "Skip".

**Icon button** `.as-icon-btn`: 44px circle, `fill-3` background, 20px glyph in label. On glass: material background. Close "X" in sheets is 30px circle with `fill-2` and a 12px bold X in `label-2`.

**FAB** `.as-fab`: 56px (or 44 in nav bar), accent fill, white plus 22px 2px stroke, colored glow shadow. The Flight log shot places a 52px blue "+" to the right of the large title, vertically centered on its cap height.

**Gradient CTA** (use sparingly, one per page): `linear-gradient(90deg,#3EC5F5,#8B6CF6)` pill, white text. Seen in Accountant "Registration / Continue".

**Store badges**: black pill-rect (radius 10), white Apple/Play glyph, two-line label 10px / 17px 600. Always pair with app product pages.

**Destructive**: red text in lists; red filled circle only for "end call" or "decline" in call UIs.

## 2. Segmented control and tabs

`.as-seg`: track `fill-3`, radius 9 (iOS 32px height) or pill. Items equal width, 13-15px 500. Selected: white thumb (dark: `#636366`), radius 7, shadow `0 3px 8px rgb(0 0 0/.12), 0 3px 1px rgb(0 0 0/.04)`. Thumb slides with spring 220ms; label weight shifts to 600.

Filter chip row (Event discovery, NeoCRM): horizontal scroll of chips, first chip "All" filled accent, others `surface-2` with a 6px colored dot before the label.

Text tabs (web nav): 14-15px label-2, active is label + optional 1.5px underline or a pill highlight (Astro "About Us" sits in a pale blue pill).

**Segmented or list?** Segmented control only when there are 2-5 options with labels of 1-2 short words and no explanation. If labels run long ("Fast 4K (upscale model)") or an option needs a hint line ("Slow. Needs the SeedVR2 weights."), use the single-choice list in section 6 instead.

## 3. Toggle, checkbox, slider

**Toggle** `.as-toggle`: 51x31 track, knob 27 white with shadow `0 3px 8px rgb(0 0 0/.15), 0 3px 1px rgb(0 0 0/.06)`. Off track `fill` gray; on track green `#34C759` (or accent). Knob slides 20px with spring; on press the knob stretches to 34px wide (liquid feel).
**Glass theme switch** (Theme switcher shot): pill 200x64 of Liquid Glass, glowing state color behind (yellow for light, indigo for dark), round glass knob with the sun/moon glyph, label in 600 weight. Knob moves with spring plus slight squash.

**Checkbox**: 22px circle (iOS style, not square). Off: 1.5px `label-3` ring. On: accent fill, white check 2px stroke, scale pop 0.8 -> 1.

**Slider**: 4px track `fill`, filled part accent, 28px white knob with e2 shadow. Media scrubber: 4px track, filled part white, knob only on hover/drag.

## 4. Fields

**Text field** `.as-field`: height 44, radius 12, fill `fill-3` (no border) or `surface` + 1px hairline when on gray canvas. 17px text, placeholder `label-3`. Focus: background to `surface`, ring `0 0 0 4px` accent 25%. Trailing icon 18px `label-2` (phone, calendar in the Accountant form).

**Search field** `.as-search`: height 36, radius 10 (or pill on marketing), magnifier 15px `label-2`, placeholder "Search", trailing mic icon. Filter button beside it as a 36px rounded square.

**Command palette** (Bellshire quick search shot, a key pattern):
- 640px wide, radius 24, thick dark material `rgb(58 58 60/.86)` + blur 40 + 0.5px light ring.
- Header: 20px search glyph, 20px placeholder "What do you want to search?", close X right.
- Hint row: keycaps (`.as-kbd`) for up/down "Navigate", return "Select", `esc` "Close" in `label-2`.
- Section labels 13px `label-2` ("Recently viewed", "Deep search", "Quick actions").
- Rows: 36px rounded-square icon tile (`surface-3`), title 17px white, subtitle 14px `label-2`. Active row: `fill` highlight radius 14 with a trailing keycap "Select".
- Deep search tokens: outline pills `key:` white + `(values)` in `label-3`.
- Quick actions: bordered pill buttons with leading 18px icon.
- Separators between sections: full-width hairline.

## 5. Chips, pills, badges, keycaps

- **Chip** `.as-chip`: height 28-32 (44 on touch, via `pointer: coarse`), pill, padding-x 12, 13-14px 500, `surface-2`. Selected: `accent-fill`, white text.
- **Status pill** `.as-status`: height 22, radius 6 (or pill), 12px 500, tint background (accent 12%), 0.5px accent 30% border optional, leading 5px dot. Colors: New/Nova = blue, Processed = purple, In process = orange, Executed = green, Refusal = red.
- **Count badge** `.as-badge`: min 20x20, pill, red `#FF3B30`, white 13px 600, 2px canvas-colored ring when overlapping an icon. Large version on app icons (the D-Studio messages icon shows a big red "1" badge overlapping the corner).
- **Keycap** `.as-kbd`: min 24x24, radius 6, `surface-3`, 0.5px ring, 12px 500 text, inner bottom shadow `inset 0 -1px 0 rgb(0 0 0/.2)`.
- **Eyebrow tag**: tiny pill with accent text and 1px accent 30% border ("CLARITY", "2026 COLLECTION" in gold on black).

## 6. Lists (inset grouped)

The Flight log and Health shots are the canonical recipe.

- Page bg `bg-grouped`. Groups are `surface` cards, radius 20 (iOS 26 style; older iOS 10), margin-x 16-20, no shadow in light mode.
- Section header above group: 20px 600 `label` ("December 2025") with 8px gap below, or 13px uppercase `label-2` for settings-style.
- Row: min height 44; with subtitle 60-64. Padding 12/16. Title 17px `label`, subtitle 15px `label-2`. Trailing value 17px `label-2` tabular ("2h 45m"), then chevron 13px 600 `label-3`.
- Separator: 0.5px hairline inset to the text start (16px, or 60px when rows have icons). Last row has none.
- Leading icon: 29-30px rounded square (radius 7) with white glyph on a system color (Settings look), or 40-48px avatar circle.
- Press state: row background `surface-3` for 120ms.
- Swipe actions (mobile): red Delete, orange Flag, blue More, full row height.

**Single-choice list** `.as-row.as-choice` (iOS Settings picker, e.g. "4K finish: Off / Fast / Quality"): the Apple answer to a radio group whose options need hint text.
- Each row is a `<label>` holding a native `<input type="radio">`, visually hidden but kept for keyboard and screen readers. Wrap the rows in `role="radiogroup"` with an `aria-label`, or a `<fieldset>` whose `<legend>` sits outside the rounded group.
- Title 17px `label` (500 when chosen), hint as `.as-row__sub` 13-15px `label-2`, allowed to wrap.
- The chosen row gets a trailing checkmark in `accent-text` (6x12 rotated stroke, 2.5px), 20px from the right edge. No radio circles, no colored row background.
- Focus: inset 2px `accent-text` ring on the row (`:has(input:focus-visible)`).

```html
<div class="as-list" role="radiogroup" aria-label="4K finish">
  <label class="as-row as-choice"><input type="radio" name="finish" value="off">
    <span class="as-row__body"><span class="as-row__title">Off (1080p)</span></span></label>
  <label class="as-row as-choice"><input type="radio" name="finish" value="fast" checked>
    <span class="as-row__body"><span class="as-row__title">Fast 4K</span></span></label>
  <label class="as-row as-choice"><input type="radio" name="finish" value="quality">
    <span class="as-row__body"><span class="as-row__title">Quality 4K</span>
    <span class="as-row__sub">Slow. Needs the SeedVR2 weights.</span></span></label>
</div>
```

**Toggle list**: same group, but each row ends in an `.as-toggle` (title + hint on the left). Use it for independent on/off options (render passes, notifications).

## 7. Cards, widgets, bento

**Card** `.as-card`: `surface`, radius 20, padding 20, e1 (light) or ring (dark). Title 17px 600, meta 13px `label-2`.

**Widget** `.as-widget` (Steps, Sleep, Stock shots):
- Sizes: small 170x170, medium 364x170, large 364x382 (iOS points). On web scale 1.0-1.3x.
- Radius 28 (squircle), padding 16-20, e2 shadow when floating on a canvas.
- Anatomy: top row = lowercase or sentence-case title 15-17px 500 `label-2` + right-aligned date range in `label-2`; hero row = big number 34-44px 700 + unit 15-17px `label-2` on the same baseline ("12.203 daily average", "8h 12m daily average"); body = chart.
- Accent widget variant: full accent background (violet `#5523EE`), all text white with 60-70% for secondary, decorative sparkles at 40% opacity, chart bars white with 25% white tracks.
- Ticker widget: black card, logo top-left, symbol in `label-2` above company name 600, price top-right 600 tabular, change in green with `+` sign; line chart with glow and a dashed reference line, tooltip as dark rounded pill.

**Bento grid** (Bento dashboard shot): grid of cards in mixed spans with 16-20 gaps, each tile a single idea (one stat, one type specimen, one image, one feature). Dark bento uses `#0B0B0C` canvas and `#161618` tiles with 0.5px rings. Mix 1 bright gradient tile per 6-8 neutral tiles.

**Feature card on marketing**: large radius 28-38, image or product render bleeding to edges, headline 28-40px 600 bottom-left, secondary text 17px gray.

## 8. Navigation

**iOS nav bar**: status bar 9:41 (SF 17 600). Large title 34 700 left-aligned at 16-20 gutter; collapses to 17 600 centered title with thin material on scroll. Trailing actions: accent FAB or text buttons.

**Back button**: chevron 17px 600 accent + previous title 17px accent.

**Web header** (Astro, Winzy, PMAT, Nuve shots): height 64-72, logo left (wordmark 600), links center 14-15px `label-2` with 28-32 gaps, actions right (text "Log in" + primary small pill "Get Started"). Becomes regular material + hairline bottom on scroll. Optional: whole header is a floating glass pill with 12px top offset.

**Sidebar (macOS / web app)**: width 220-260, material or `surface-2`, section labels 11px 600 uppercase `label-3` ("LIBRARY", "DISCOVER"), rows 28-32px with 16px icon + 13-14px label, selected row = accent 15% tint or `fill` pill with accent icon (NeoCRM uses a pale blue rounded rectangle with 1px blue border).

**Tab bar**: 49pt + home indicator, thin material, 5 items max, icon 24 + label 10px 500. Selected = accent, others `label-2`. iOS 26 style: floating glass capsule with the selected item in a lighter inner pill.

**Floating dock / toolbar** (visionOS Discord shot, player shot): glass capsule, 56-64 high, 8px padding, items are 44px circles; destructive item red circle, active item white circle with dark glyph, primary item green pill with icon + label.

**Window chrome (macOS)**: radius 12-14 (Tahoe: 26 for larger windows), traffic lights 12px circles `#FF5F57`, `#FEBC2E`, `#28C840` with 8px gaps at 20/20 offset, 0.5px dark ring. Title 13px 600 centered or omitted (unified toolbar).

## 9. Overlays

- **Sheet**: radius 28-38 top corners, grabber 36x5 `label-3` pill 6px from top, background `surface` or thick material, enters from bottom with `ease-out` 400ms.
- **Modal (web)**: 480-640 width, radius 24, padding 24-28, scrim `rgb(0 0 0/.25)` + 8px backdrop blur. Primary action bottom-right pill, secondary text button.
- **Popover / menu**: regular material, radius 14, padding 6, items 32px radius 8, 14px label, hover = accent fill with white text (macOS) or `fill-3` (iOS).
- **Toast / notification** (Bento shot alerts, Health lock screen): glass or `surface` card radius 20, 40px app icon tile, title 15px 600, body 13-15px `label-2`, timestamp right-aligned 13px `label-3`. Stack with 8px gap, slide-down + fade.
- **Lock-screen style alert**: big time 72-96px 300-600 on photo, actions as circular 60px buttons with label below (red X "Postpone", blue check "Open Health").

## 10. Data

- **Stat**: number 28-56px 700 tabular, label 13px `label-2` below or a delta chip beside (`+12%` green tint pill with arrow). Server health "98%" + "^12" green, API "120ms" + "5%".
- **Capsule bar chart**: bars are pills, width 10-16 (or ~45% of slot), gaps equal; each bar has a full-height `fill-4` track; fill grows from bottom with spring and 40ms stagger. Axis labels 13px `label-3` centered below. No gridlines.
- **Segmented bar meter** (API execution): row of 8-12 short pills, filled ones accent, rest `fill-3`.
- **Line chart**: 2.5px line, round joins, accent color, area fill gradient from accent 35% to 0, optional `filter: drop-shadow(0 0 8px accent)` glow on dark. Reference line 1px dashed `label-3`. Tooltip: dark pill radius 10, 15px 600 white tabular, 8px white dot with accent ring on the line.
- **Ring / gauge**: 10-14px stroke, round caps, track `fill-3`, start at -90deg, counter-clockwise for Activity look; percent label center 20-28px 700.
- **Progress bar**: 4-6px pill, accent fill.
- **Tables** (NeoCRM): header 12px 500 `label-2` no background, rows 44-48 with hairlines, avatar 24 + name, status pills, trailing eye icon `label-3`. Zebra stripes never.

## 11. Media

- **Player bar** (MUSE, Negi player shots): glass capsule or bottom bar, album art 40-56 radius 8-10, title 15 600 + artist 13 `label-2`, controls 28-32 glyphs (prev/play/next), scrubber 4px with white fill, volume/AirPlay/queue icons right.
- **Album/artist tile**: square image radius 10-12, title 13-15 600 below, year 12 `label-3`, a small pink 24px circular play button overlapping bottom-right of the art.
- **Avatar**: circle, 0.5px inner ring `rgb(0 0 0/.08)`, online dot 10-12 green with 2px surface ring. Memoji-style 3D avatars fit the style well.
- **Device frame**: phone radius 48-56 with 10-12 black bezel and subtle metal rim gradient; Dynamic Island 120x36 pill. Laptop renders at 3/4 isometric angle with soft floor shadow.

## 12. App icons and marks

- Canvas 1024, squircle radius ~22.4% (iOS mask), safe glyph area 60-70%.
- Background: vertical gradient of one hue (top 8-12% lighter) or a 2-3 stop mesh (pink -> violet -> teal) for creative apps.
- Glyph: chunky, simple, slightly 3D: inner highlight at top, soft inner shadow at bottom, 1-2 stops gradient. Liquid Glass glyphs are translucent with refraction and a bright specular edge (Majik icon: two glass triangles with warm orange-pink core).
- Light/Dark/Tinted variants: dark variant uses graphite `#3A3A3C` -> `#636366` base with white glyph.
- Badge: red circle 30% of icon width, overlapping top-right by 25%.
- Logo marks (Abstract tech logo shot): soft-gradient petals or blades with 20-40% translucency, overlapping to create new tints, inside a squircle tile.
