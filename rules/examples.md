---
name: examples
description: HyperFrames starter examples - templates for common video styles and use cases
metadata:
  tags: examples, templates, starter, scaffold, init
---

## Initializing with a starter example

```bash
npx hyperframes init my-video --example <name>
```

## Available examples

### Blank

Minimal scaffolding — start from scratch.

```bash
npx hyperframes init my-video --example blank
```

Use this when you have a clear design in mind and want full control.

---

### warm-grain

Cream-toned aesthetic with grain texture overlay. Best for: lifestyle, branding, editorial.

```bash
npx hyperframes init my-video --example warm-grain
```

Key patterns: CSS grain overlay, warm color grading, soft fade-in typography.

---

### play-mode

Energetic elastic animations. Best for: social media promos, product drops, gaming.

```bash
npx hyperframes init my-video --example play-mode
```

Key patterns: `back.out` and `elastic.out` easing, bold color pops, staggered element reveals.

---

### swiss-grid

Grid-based layout following International Typographic Style. Best for: tech brands, B2B, SaaS.

```bash
npx hyperframes init my-video --example swiss-grid
```

Key patterns: strict grid layout, Helvetica-style typography, minimal color palette.

---

### kinetic-type

Bold kinetic typography promo with dramatic text animations. Best for: trailers, event promos, announcements.

```bash
npx hyperframes init my-video --example kinetic-type
```

Key patterns: large display type, letter-by-letter stagger, fast cuts with GSAP.

---

### decision-tree

Flowchart with branching paths and progressive reveals. Best for: explainers, tutorials, data storytelling.

```bash
npx hyperframes init my-video --example decision-tree
```

Key patterns: SVG paths drawn on, sequential node reveals, connecting lines.

---

### product-promo

Multi-scene product showcase with SVG assets. Best for: e-commerce, app demos, product launches.

```bash
npx hyperframes init my-video --example product-promo
```

Key patterns: multiple scenes with transitions, product image scale-in, price tag pop, CTA slide-up.

---

### nyt-graph

Animated data chart in print editorial style. Best for: data journalism, reports, infographics.

```bash
npx hyperframes init my-video --example nyt-graph
```

Key patterns: SVG bar/line chart, staggered bar reveals, editorial typography.

---

### vignelli (portrait)

Bold typography with red accents. 1080×1920. Best for: Instagram Reels, TikTok, announcements.

```bash
npx hyperframes init my-video --example vignelli
```

Key patterns: portrait canvas, large headline, strong accent color, minimal layout.

---

## Choosing the right example

| Goal                              | Recommended example    |
|-----------------------------------|------------------------|
| Quick product ad                  | `product-promo`        |
| Social media content              | `play-mode` or `vignelli` |
| Data story / infographic          | `nyt-graph` or `decision-tree` |
| Brand storytelling                | `warm-grain`           |
| Event / launch announcement       | `kinetic-type`         |
| Corporate / B2B explainer         | `swiss-grid`           |
| Full custom design                | `blank`                |

## Listing all examples

```bash
npx hyperframes examples
```
