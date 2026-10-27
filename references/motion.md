# Motion

Twelve of the 64 analyzed shots were motion studies (Negi Design player, health app, motion graphic study, liquid glass gaming, glassy icon animation, theme switcher, logo animations, SaaS intro, product launch promo, Shopify Apple scroll, AETHER watch, Bento interaction). The common feel: **physical, calm, decisive**. Things move like they have mass, settle once, and never wobble.

## Contents
1. Principles
2. Curves (CSS ready)
3. Interaction states
4. Entrances and reveals
5. Text animation
6. Number and chart animation
7. Scroll-driven storytelling
8. Shared-element and morph transitions
9. Reduced motion
10. Library equivalents (Framer Motion, GSAP, SwiftUI, Qt, Remotion)

---

## 1. Principles

1. **Springs for anything the user touches**; curves for things that just appear.
2. **Short distances.** Rise 8-24px, scale from .96-.98, never fly in from off-screen on web.
3. **Opacity + blur together.** Apple reveals unblur as they fade (`filter: blur(8px)` -> 0). This is the most "Apple" single trick.
4. **Stagger 30-60ms** between siblings; cap total stagger at ~400ms.
5. **One hero motion per view.** Everything else is quiet.
6. **Interruptible.** Hover off mid-animation should reverse smoothly; use transitions, not one-shot keyframes, for state.

## 2. Curves

```css
:root {
  --as-ease: cubic-bezier(.25,.1,.25,1);
  --as-ease-out: cubic-bezier(.32,.72,0,1);      /* iOS sheet / drawer */
  --as-ease-in-out: cubic-bezier(.65,0,.35,1);
  /* Damped spring, damping .8, response .4s: 1.5% overshoot, settle ~510ms */
  --as-spring: linear(0, .047, .156, .292, .433, .564, .678, .773, .847, .904, .946, .975, .994, 1.006, 1.012, 1.015, 1.015, 1.014, 1.012, 1.01, 1.008, 1.006, 1.004, 1.003, 1);
  --as-spring-dur: 510ms;
  /* Bouncier spring, damping .65, response .45s: 7% overshoot, settle ~700ms. Toggles, knobs, badges. */
  --as-spring-bouncy: linear(0, .07, .23, .422, .609, .769, .893, .979, 1.032, 1.06, 1.068, 1.064, 1.054, 1.041, 1.028, 1.017, 1.008, 1.002, .998, .996, .995, .996, .996, .997, 1);
  --as-spring-bouncy-dur: 700ms;
}
```

`linear()` is supported in all evergreen browsers since 2023. Fallback: `--as-ease-out`.

## 3. Interaction states

| State | Change | Timing |
|---|---|---|
| Hover (pointer) | bg tint +4% or brightness 1.05; cards lift 2px and shadow e2 -> e3 | 200ms ease |
| Press | `scale(.97)` buttons, `scale(.98)` cards, bg `surface-3` for rows | 120ms ease-out |
| Release | back to 1 | spring |
| Focus | 3px `accent-text` outline, 2px offset (inset inside clipped lists), appears instantly | 0-100ms |
| Toggle | knob slides; knob stretches 27 -> 34px wide while pressed; track color crossfade | spring-bouncy |
| Segmented | thumb slides under the new item | spring 300-400ms |
| Disclosure | chevron rotates 90deg | 250ms ease-in-out |

## 4. Entrances and reveals

```css
.as-reveal { opacity: 0; transform: translateY(16px) scale(.98); filter: blur(8px);
  transition: opacity .7s var(--as-ease-out), transform .9s var(--as-ease-out), filter .7s var(--as-ease-out); }
.as-reveal.is-in { opacity: 1; transform: none; filter: none; }
```

```js
// Reveal on scroll, staggered by DOM order within each group.
const io = new IntersectionObserver(es => es.forEach(e => {
  if (!e.isIntersecting) return;
  const kids = e.target.querySelectorAll('.as-reveal');
  (kids.length ? kids : [e.target]).forEach((el, i) => setTimeout(() => el.classList.add('is-in'), i * 50));
  io.unobserve(e.target);
}), { threshold: .2 });
document.querySelectorAll('[data-reveal]').forEach(el => io.observe(el));
```

- **Sheet/modal**: translateY(100%) -> 0 with `--as-ease-out` 450ms; scrim fades 250ms. Modal on web: scale .96 -> 1 + fade, 300ms.
- **Popover/menu**: scale .9 -> 1 from the anchor (`transform-origin` at the trigger), opacity, 200ms spring.
- **Toast**: slide down 12px + fade, auto-hide 4s, exit fade 200ms.
- **App icon / logo intro** (Majik, Glassy icon, logo animation shots): icon scales .6 -> 1 with spring-bouncy, specular highlight sweeps across (animated gradient position), then badge pops.

## 5. Text

- **Word-by-word fade-up**: split headline into spans, each word rises 12px + unblurs, 40ms stagger. (SaaS intro "Ready for a Whole...", Apple keynote style.)
- **Gradient sweep**: text `background: linear-gradient(90deg, var(--label) 0 40%, var(--accent) 55%, transparent 75%)` with `background-size: 250% 100%`, animate `background-position` from 100% to 0 over 1.2s. Reads as text "lighting up".
- **Tagline beats**: show one short phrase at a time ("Sound." / "Refined."), each holding 600-900ms, crossfade 300ms. For video and hero loops.
- **Kinetic type** (TRY shot): bold uppercase words cut on the beat, wide tracking .1em, black background, no easing on cuts, eased scale 1.02 -> 1 on each new word.

## 6. Numbers and charts

- Count-up numbers over 800-1200ms with ease-out, tabular numerals so width does not jitter.
- Bars grow from 0 height with spring, 40ms stagger left to right.
- Line charts draw with `stroke-dasharray` / `stroke-dashoffset` over 1.2s ease-in-out, then the area gradient fades in 300ms.
- Ring gauges animate `stroke-dashoffset` with spring-bouncy for a satisfying close.
- Live value change (stock price): crossfade old/new number with 6px vertical slide; flash the delta pill tint 300ms.

## 7. Scroll-driven storytelling (Apple product page)

The "Luxury Shopify Apple Scroll" and AETHER shots replicate apple.com product pages:

- A sticky full-viewport stage (`position: sticky; top: 0; height: 100vh`) inside a tall section (300-500vh).
- Scroll progress drives: product rotation (image sequence on canvas, 60-150 frames), headline opacity, scale 1.15 -> 1, background darkening.
- Use CSS scroll-driven animations where possible:

```css
@supports (animation-timeline: view()) {
  .as-scroll-zoom { animation: as-zoom linear both; animation-timeline: view(); animation-range: entry 0% cover 60%; }
  @keyframes as-zoom { from { transform: scale(1.15); opacity: 0 } to { transform: scale(1); opacity: 1 } }
}
```

- Fallback: IntersectionObserver reveal. Never hijack the scroll wheel; scroll speed must stay native.

## 8. Morph and shared-element

- Card -> detail: shared image grows to the hero position (View Transitions API: `view-transition-name` on both elements), radius morphs 20 -> 0, 450ms `--as-ease-out`.
- Player capsule expands into full player (Negi player): width/height + radius morph, content crossfades at 40% of the way.
- Liquid glass blobs merging (gaming win card, toggle): two glass shapes with an SVG goo filter (`feGaussianBlur` + `feColorMatrix` alpha 18 -7) so they fuse as they approach.

## 9. Reduced motion

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation-duration: .01ms !important; animation-iteration-count: 1 !important; transition-duration: .01ms !important; scroll-behavior: auto !important; }
  .as-reveal { opacity: 1; transform: none; filter: none; }
}
```

Keep opacity crossfades (they do not trigger vestibular issues), drop movement, zoom and parallax.

## 10. Library equivalents

| Target | Default spring | Snappy |
|---|---|---|
| Framer Motion | `{ type: "spring", stiffness: 260, damping: 30 }` (or `bounce: .15, duration: .5`) | `{ stiffness: 400, damping: 32 }` |
| GSAP | `ease: "power3.out"` 0.6s for reveals; `"back.out(1.2)"` for pops | `"expo.out"` 0.4s |
| SwiftUI | `.spring(response: 0.4, dampingFraction: 0.8)` or `.smooth` | `.snappy` / `.bouncy` |
| Qt (PySide) | `QEasingCurve.OutCubic` 220ms; `OutBack` (overshoot 1.2) for knobs | `OutQuint` 160ms |
| Remotion | `spring({ frame, fps, config: { damping: 200 } })` for calm; `{ damping: 14, mass: .6 }` for pops | |
