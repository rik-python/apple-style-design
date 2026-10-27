# Layouts and recipes by output type

Pick the recipe that matches what the user asked for. Each lists structure, measurements and the signature details that make it read as Apple style.

## Contents
1. Marketing landing page
2. Product page with scroll story
3. SaaS / dashboard web app
4. Mobile app screens (iOS)
5. Widgets
6. Desktop app (macOS style) and plugin panels
7. Spatial / visionOS style
8. Posters, social, slides
9. Icons and logo marks
10. Copywriting rules

---

## 1. Marketing landing page

Seen in: Pluzz, Astro, ai_scripts, Winzy, PMAT, Nuve, MUSE, AETHER, Swiss Chronograph.

```
[ floating header: logo · 3-5 links · Log in + primary pill ]
[ HERO: eyebrow · 2-line headline (two-tone) · 1-2 line lead · CTA pair · trust row ]
[ product visual: device mockup / render / dashboard card stack, bleeding toward edges ]
[ logo strip: 5-7 grayscale logos at 40-50% opacity, "Used by 100+ brands" caption ]
[ feature bento grid (2-3 rows) ]
[ big statement section: one sentence, 48-72px, centered, lots of air ]
[ stats row: 3-4 big numbers with gray captions ]
[ testimonial or showcase carousel ]
[ final CTA band on mesh gradient or dark ]
[ footer: 4 columns of 13px links in label-2, hairline on top ]
```

Signature details:
- Hero centered (product/tool) or left-aligned with image right (service/people). Headline 56-88px, max 2 lines, `text-wrap: balance`.
- CTA pair: primary pill + secondary (outline or ghost with chevron). 12-16 gap.
- Page sits as a rounded "browser card" (radius 20-28, e2 shadow) on a soft canvas in Dribbble presentations. In production, the page is full bleed; reuse the rounded card for embedded screenshots.
- Stats with icons in thin outline (Nuve: 95% / 30+ / 7-day right column).
- Floating UI chips over hero imagery (Winzy notification cards on portraits, PMAT chat + satisfaction gauge overlapping the photo): small white cards radius 14, e2 shadow, 12-13px text.

## 2. Product page with scroll story

For a hero product (hardware, plugin, app): see `motion.md` section 7.

- Section 1: product name 80-120px 700, tagline 28px gray, price/date line, two CTAs.
- Sticky stage where the product rotates/zooms while 3-4 short statements fade in and out (one at a time, 40-56px).
- Spec grid: "big number + small label" tiles, 3 or 4 across.
- Color picker: 28px circles with 2px ring on selected, product image crossfades.
- Dark section for "pro" features, light for everyday features. Alternate.

## 3. SaaS / dashboard web app

Seen in: Bento dashboard, Bellshire, NeoCRM, ai_scripts dashboards, pitch deck.

- Layout: sidebar 240 + content; content padding 24-32; top bar 64 with page title 28px 600 left, search + bell + avatar right.
- Cards in a 12-col grid, gaps 16-20, radius 20, light mode on `#F5F5F7` canvas with white cards, or dark `#0B0B0C` with `#161618` cards.
- Card header: title 15-17 600 + period dropdown pill on the right ("Last 30 days v").
- Stat cards: big number + delta pill + mini chart.
- Tables: see components section 10. Primary action: top-right pill with "+" icon ("ADD APPLICATION").
- Command palette on Cmd/Ctrl+K (components section 4). This one feature makes any web app feel Apple-grade.
- Empty states: 64px SF-style glyph in `label-3`, 20px title, 15px gray body, one tinted button.

## 4. Mobile app screens (iOS)

Seen in: Flight log, Health reminders, Direct messaging, Event discovery, Accountant, Task manager.

- Frame 393x852 (iPhone 15/16 Pro). Status bar 54, home indicator 34.
- Large title screen: title 34 700 at y=~100, content starts 16 below.
- Inset grouped lists for data; avatar lists for people (chats: 52px avatar, name 17 600, preview 15 `label-2` one line, time 15 `label-2` right, unread badge accent circle).
- Chat bubbles: radius 20 with 6px tail corner, outgoing accent (`#007AFF` or brand like `#242FF1`) white text, incoming `#E9E9EB` (dark `#26252A`) label text, max width 75%, read receipt 11px `label-3` under.
- Onboarding: illustration/3D top 55%, headline 28-34 700 bottom-left, 15-17 body gray, primary pill full width at the bottom 16 inset, secondary text button below.
- Bottom sheet over maps (Event discovery): grabber, title 20 600, meta rows with 16px icons, heart toggle red, "See More" accent link.
- Tab bar 5 items or floating glass tab bar (iOS 26).

## 5. Widgets

See components section 7. Sizes on web: small 170, medium 364x170, large 364x382 (scale x1.2 for desktop showcase). Present on `#F5F5F7` canvas with e2 shadow, or on a wallpaper with glass.

Widget ideas that fit: stat + capsule bars (activity, steps, sleep, sales), ticker line, next event, now playing, weather (gradient sky by condition), single big number countdown ("Day 13"), quick actions (2x2 rounded square buttons).

## 6. Desktop app (macOS) and plugin panels

Seen in: MUSE desktop player, MAC game menu, AeroDash.

- Window: radius 12-26, traffic lights, unified toolbar 52 tall, sidebar 220 translucent with section labels uppercase 11px `label-2`.
- Dense type: body 13px, headline 13px 600, titles 20-28px. Controls 28-32 high.
- Content tiles: album grid 120-160px squares, 16-20 gap, title + year below.
- Bottom transport/player bar 64-72 high with scrubber spanning the center.
- **Plugin panels** (Nuke PySide, ComfyUI sidebar, DCC tools): treat as macOS inspector. 13px type, 28px controls, grouped sections in `surface-2` cards radius 10, section headers 11px uppercase `label-3`, sliders with value fields 56 wide on the right, one accent for the primary "Apply/Render" pill at the bottom. Dark mode by default for VFX hosts. Recipes per platform: `platforms.md`.

## 7. Spatial / visionOS style

Seen in: Discord visionOS, liquid glass gaming card.

- Windows are glass panes (regular material, no solid bg) radius 46, floating over a real environment photo.
- Ornaments: tab bar as a vertical glass capsule floating left of the window; toolbar as a glass capsule below the window.
- Text white, secondary white 60%. Hover = soft light lift (brighter fill), no color change.
- Window bar: 6x6 dot + 120px pill handle centered below the window.

## 8. Posters, social, slides

Seen in: AirPods poster, Coming Soon card, Day 13, print ads motion, pitch deck, App Store promo art.

- Composition: one product/hero object, one headline, one line of support, lots of negative space. Product color drives the whole palette (lilac iPhone -> lilac stage).
- Headline 6-10% of canvas height, 600-700, tight tracking; support line 40% of headline size, 70% opacity.
- Glass/3D type for titles (Day 13: frosted translucent extruded letters with sparkles).
- Slides: 16:9, dark `#000`/`#0B0B0C` or white, one idea per slide, big number slides ("1.3M", "22%", "640K") with tiny captions, screenshots in device frames tilted in 3D for energy.
- Social carousels: consistent card radius 28, same mesh background family across slides.

## 9. Icons and marks

See components section 12 and materials section 9. Deliver 1024 squircle PNG + light/dark/tinted variants when asked for an app icon. For UI icons use an SF Symbols-like open set (Lucide at 1.5 stroke) and keep one weight across the product.

## 10. Copywriting rules

- Headlines: 2-7 words or one clear question. Periods allowed and encouraged on taglines.
- Patterns that worked in the shots: "Sound. Refined." · "New iPhone. Coming Soon." · "Timeless Precision" · "Hear Everything" · "Unlock your skin's potential" · "Manage finances easily & quickly" · "Discover all events in one app" · "Everyday is a step."
- Benefits over features; numbers as proof ("95% accurate", "13h 50m", "+1,25%").
- Buttons: verb first, 1-2 words: "Get started", "Learn more", "Buy", "Notify me", "Continue", "Explore", "Analyze Skin".
- Sentence case everywhere (except tiny uppercase section labels and deliberate eyebrows).
- No exclamation marks except celebratory moments ("Congratulations!").
- Placeholder text should be real and specific (flight routes, real-looking names, plausible prices), never lorem ipsum.
