---
name: animations
description: GSAP animations in HyperFrames - timelines, easing, properties, registration
metadata:
  tags: animations, gsap, timeline, easing, opacity, scale, position
---

All animations in HyperFrames MUST use **GSAP** (GreenSock Animation Platform).

CSS transitions and CSS `animation` properties are FORBIDDEN — they will not render correctly frame-by-frame.

## GSAP timeline rules

1. Every GSAP timeline MUST be created with `{ paused: true }`
2. Every timeline MUST be registered on `window.__timelines` with a unique key matching the clip's `id`

```html
<script src="https://cdn.jsdelivr.net/npm/gsap@3/dist/gsap.min.js"></script>
<script>
  window.__timelines = window.__timelines || {};

  const tl = gsap.timeline({ paused: true });

  tl.fromTo("#title",
    { opacity: 0, y: 40 },
    { opacity: 1, y: 0, duration: 0.6, ease: "power2.out" }
  );

  window.__timelines["title"] = tl;
</script>
```

## Common animations

### Fade in

```js
const tl = gsap.timeline({ paused: true });
tl.fromTo("#el", { opacity: 0 }, { opacity: 1, duration: 0.5, ease: "power2.out" });
window.__timelines["el"] = tl;
```

### Slide up + fade in

```js
const tl = gsap.timeline({ paused: true });
tl.fromTo("#el",
  { opacity: 0, y: 60 },
  { opacity: 1, y: 0, duration: 0.6, ease: "power3.out" }
);
window.__timelines["el"] = tl;
```

### Scale pop

```js
const tl = gsap.timeline({ paused: true });
tl.fromTo("#el",
  { scale: 0.7, opacity: 0 },
  { scale: 1, opacity: 1, duration: 0.5, ease: "back.out(1.7)" }
);
window.__timelines["el"] = tl;
```

### Staggered list

```js
const tl = gsap.timeline({ paused: true });
tl.fromTo(".item",
  { opacity: 0, x: -30 },
  { opacity: 1, x: 0, duration: 0.4, stagger: 0.1, ease: "power2.out" }
);
window.__timelines["list"] = tl;
```

## Easing guide

| Feel         | GSAP ease             |
|--------------|-----------------------|
| Smooth       | `power2.out`          |
| Snappy       | `power3.out`          |
| Bouncy       | `back.out(1.7)`       |
| Elastic      | `elastic.out(1, 0.5)` |
| Linear       | `none`                |
| Ease in-out  | `power2.inOut`        |

## Multiple timelines

Each animated clip element should have its own timeline registered with its `id`:

```html
<div id="headline" class="clip" data-start="1" data-duration="7" data-track-index="2" ...>Headline</div>
<div id="subtitle" class="clip" data-start="1.5" data-duration="6" data-track-index="2" ...>Subtitle</div>

<script>
  window.__timelines = window.__timelines || {};

  const tlHead = gsap.timeline({ paused: true });
  tlHead.fromTo("#headline", { opacity: 0, y: -20 }, { opacity: 1, y: 0, duration: 0.5 });
  window.__timelines["headline"] = tlHead;

  const tlSub = gsap.timeline({ paused: true });
  tlSub.fromTo("#subtitle", { opacity: 0 }, { opacity: 1, duration: 0.4, delay: 0.2 });
  window.__timelines["subtitle"] = tlSub;
</script>
```

## Exit animations (fade out before clip ends)

To animate out before `data-duration` ends, add a delayed tween:

```js
const tl = gsap.timeline({ paused: true });
// Fade in at start
tl.fromTo("#card", { opacity: 0, y: 30 }, { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" });
// Fade out 0.5s before clip ends (clip duration = 5s)
tl.to("#card", { opacity: 0, y: -20, duration: 0.4, ease: "power2.in" }, 4.6);
window.__timelines["card"] = tl;
```

## Multi-step sequence

Chain multiple tweens on the same or different elements:

```js
const tl = gsap.timeline({ paused: true });
tl.fromTo("#logo",     { scale: 0, opacity: 0 }, { scale: 1, opacity: 1, duration: 0.4, ease: "back.out(2)" })
  .fromTo("#headline", { opacity: 0, y: 20 },    { opacity: 1, y: 0, duration: 0.5 }, "+=0.1")
  .fromTo("#subline",  { opacity: 0 },            { opacity: 1, duration: 0.4 }, "+=0.05")
  .fromTo("#cta",      { opacity: 0, scale: 0.8 }, { opacity: 1, scale: 1, duration: 0.35, ease: "back.out(1.5)" }, "+=0.2");
window.__timelines["intro-sequence"] = tl;
```

## Synchronous-only rule

GSAP timelines MUST be constructed fully synchronously. Never use `async/await`, `fetch`, or `setTimeout` inside timeline setup — the renderer cannot wait for async operations.

```js
// FORBIDDEN
fetch('/data.json').then(() => {
  const tl = gsap.timeline({ paused: true }); // will not render correctly
  window.__timelines["el"] = tl;
});
```

## Audio-reactive animations

Map frequency bands to visual properties using the `data-audio-reactive` attribute:

```html
<div id="bar"
     class="clip"
     data-start="0"
     data-duration="10"
     data-track-index="1"
     data-audio-reactive="bass:scale,treble:opacity"
     style="width: 100px; height: 100px; background: red;">
</div>
```

Frequency bands: `bass`, `mid`, `treble`  
Visual properties: `scale`, `opacity`, `glow`, `brightness`
