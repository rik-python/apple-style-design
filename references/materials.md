# Materials: Liquid Glass, frosted, gradients, grain

Glass appeared in more than a third of the analyzed shots (visionOS Discord, quick search modal, theme switcher, liquid glass video/photo pills, gaming win card, glass app icons, wallet stamp icon, player capsule). It is the single most recognizable "2025-2026 Apple" signal.

## Contents
1. When to use glass
2. Frosted material (baseline)
3. Liquid Glass (CSS)
4. Liquid Glass with refraction (SVG filter, Chromium)
5. Glass on light vs dark vs photo
6. Mesh gradient backdrops
7. Grain and noise
8. Glow
9. 3D glossy objects (icons, glyphs)

---

## 1. When to use glass

Use glass for layers that float above content: toolbars, tab bars, docks, players, popovers, sheets, command palettes, floating headers, toggles on hero imagery. Do not use it for primary content cards in lists or for long text blocks: legibility drops and the effect loses meaning.

Glass needs something behind it. Over a flat white page it reads as a gray box. Put a photo, video, gradient mesh or colorful content behind any glass layer.

## 2. Frosted material

```css
.as-material {
  background: rgb(250 250 252 / .72);
  -webkit-backdrop-filter: blur(30px) saturate(180%);
  backdrop-filter: blur(30px) saturate(180%);
  box-shadow: 0 0 0 .5px rgb(0 0 0 / .06);
}
@media (prefers-color-scheme: dark) {
  .as-material { background: rgb(40 40 42 / .72); box-shadow: 0 0 0 .5px rgb(255 255 255 / .08); }
}
```

`saturate(180%)` matters: it keeps colors behind the blur vivid instead of muddy, which is the Apple look.

## 3. Liquid Glass (CSS only, all modern browsers)

Anatomy (from the shots): clear body with very light tint, bright 1px top/left edge highlight, darker bottom inner edge, soft outer shadow, a faint specular gradient sweeping from top-left.

```css
.as-glass {
  position: relative;
  background:
    linear-gradient(135deg, rgb(255 255 255 / .28), rgb(255 255 255 / .06) 40%, rgb(255 255 255 / .02) 60%, rgb(255 255 255 / .14));
  -webkit-backdrop-filter: blur(18px) saturate(190%) brightness(1.06);
  backdrop-filter: blur(18px) saturate(190%) brightness(1.06);
  border-radius: 999px;
  box-shadow:
    inset 0 1px 0 rgb(255 255 255 / .65),    /* top specular edge */
    inset 1px 0 0 rgb(255 255 255 / .25),    /* left edge */
    inset 0 -1px 0 rgb(255 255 255 / .12),   /* bottom rim */
    inset 0 -10px 20px -10px rgb(255 255 255 / .18), /* inner bottom glow */
    0 8px 32px rgb(0 0 0 / .18),             /* lift */
    0 1px 2px rgb(0 0 0 / .10);
}
.as-glass::after {           /* rim light: thin bright border fading around the shape */
  content: ""; position: absolute; inset: 0; border-radius: inherit; padding: 1px;
  background: linear-gradient(160deg, rgb(255 255 255 / .8), rgb(255 255 255 / .1) 35%, rgb(255 255 255 / 0) 60%, rgb(255 255 255 / .35));
  -webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
  -webkit-mask-composite: xor; mask-composite: exclude;
  pointer-events: none;
}
```

Tinted glass (e.g. the pink VIDEO/PHOTO pills): add `background-color: color-mix(in srgb, var(--tint) 35%, transparent)` under the gradient. Selected item inside a glass group = a second, lighter glass pill nested inside (`rgb(255 255 255/.25)`), text switches to the accent (yellow "PHOTO" in the shot).

Dark glass (quick search modal): `background: rgb(58 58 60 / .82)`, same blur, top highlight at 0.18 alpha, ring `0 0 0 .5px rgb(255 255 255/.12)`.

## 4. Refraction (Chromium only, progressive)

True Liquid Glass bends the background at the edges. Chrome/Edge support SVG filters inside `backdrop-filter`. Wrap it in `@supports` and keep section 3 as the fallback.

```html
<svg width="0" height="0" style="position:absolute">
  <filter id="as-refract" x="0" y="0" width="100%" height="100%">
    <feTurbulence type="fractalNoise" baseFrequency="0.008 0.012" numOctaves="2" seed="7" result="n"/>
    <feGaussianBlur in="n" stdDeviation="2" result="nb"/>
    <feDisplacementMap in="SourceGraphic" in2="nb" scale="38" xChannelSelector="R" yChannelSelector="G"/>
  </filter>
</svg>
```

```css
@supports (backdrop-filter: url(#as-refract)) {
  .as-glass--refract { backdrop-filter: url(#as-refract) blur(6px) saturate(190%); }
}
```

Keep `scale` 20-50. Higher looks like a broken screen. Test that text behind still reads as shapes.

## 5. Glass on different backgrounds

| Behind | Body tint | Top highlight | Text |
|---|---|---|---|
| Photo / video | white 8-20% | .6-.75 | white 600 with `text-shadow: 0 1px 2px rgb(0 0 0/.25)` |
| Mesh gradient | white 15-25% | .7 | white or label |
| Light UI | white 55-72% (becomes frosted) | .9 | label |
| Dark UI | `#3A3A3C` 70-85% | .15-.2 | white |

## 6. Mesh gradient backdrops

Seen in: Majik icon stage, Accountant periwinkle stage, Day 13 counter, MUSE purple stages, flight log wallpaper, SaaS intro peach, App Store promo blue.

```css
.as-mesh {
  background:
    radial-gradient(60% 50% at 15% 20%, #8E7CFF 0%, transparent 60%),
    radial-gradient(50% 45% at 85% 25%, #FF7AB6 0%, transparent 60%),
    radial-gradient(55% 55% at 70% 85%, #FFB86B 0%, transparent 60%),
    radial-gradient(60% 60% at 20% 90%, #4FD1C5 0%, transparent 60%),
    #2B2A6B;
}
```

Palettes that matched the shots:
- **Aurora** (Majik): `#2B2A6B` base, `#8E7CFF`, `#FF7AB6`, `#FFB86B`, `#4FD1C5`.
- **Lilac** (Coming Soon, MUSE): `#3B2F5C` base, `#CFB9EB`, `#9D88BB`, `#6C4CF5`.
- **Peach dawn** (SaaS intro): `#FFF7F2` base, `#F6D7B8`, `#F9E1E6`, `#E8EEFF`.
- **Lagoon** (Flight log wallpaper): `#1D3F9E`, `#2F6BD6`, `#7FD3D6`, `#BFEDEA`.
- **Periwinkle** (Accountant): flat `#8D9DEE` with a blurred 3D object behind cards.

Animate slowly (20-40s) by moving gradient centers with `@property` registered percentages, or rotate a blurred blob layer. Never fast.

## 7. Grain

A 3-6% noise overlay removes gradient banding and adds a premium print feel (Day 13, MUSE stages).

```css
.as-grain::before {
  content: ""; position: absolute; inset: 0; pointer-events: none; opacity: .06; mix-blend-mode: overlay;
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='160' height='160'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='.9' numOctaves='3' stitchTiles='stitch'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>");
}
```

## 8. Glow

- Colored shadow under accent elements: `0 8px 24px color-mix(in srgb, var(--accent) 40%, transparent)`.
- Data glow on dark: `filter: drop-shadow(0 0 6px #30D158)` on the line + area gradient under it.
- State glow behind glass (theme switch yellow, wallet stamp cyan): a blurred `radial-gradient` of the state color, 40-60px blur, 50-70% opacity, positioned behind the glass element.
- Edge glow on dark glass icons (WalletStamp): 1px cyan inner border + 24px cyan outer shadow at 40%.

## 9. 3D glossy objects

For icons, hero glyphs and badges (Settings gears, Messages bubble, Health heart, Majik triangles):

- Base gradient top-light to bottom-dark of one hue (8-15% lightness range).
- Inner highlight: `inset 0 2px 0 rgb(255 255 255/.5)` plus a radial white spot at top-left 30%.
- Inner shadow at the bottom edge: `inset 0 -4px 8px rgb(0 0 0/.15)`.
- Contact shadow below: ellipse, blur 20-30, 20% black.
- Clay/puffy look (Messages bubble, Health heart): large blur soft shading, almost no specular, slightly desaturated colors.
- For real 3D renders, prompt image models with: "soft 3D clay render, Apple app icon style, frosted glass, studio lighting, subtle specular highlight, pastel gradient background, high detail, centered" and composite onto the squircle.
