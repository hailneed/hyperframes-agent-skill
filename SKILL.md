---
name: hyperframes
description: Best practices for HyperFrames - Write HTML, Render video. Built for agents.
metadata:
  tags: hyperframes, heygen, video, html, animation, composition, gsap
---

## When to use

Use this skill whenever you are working with HyperFrames compositions to obtain domain-specific knowledge and avoid common mistakes.

## New project setup

When in an empty folder or workspace with no existing HyperFrames project, scaffold one using:

```bash
npx hyperframes init my-video
```

Replace `my-video` with a suitable project name.

## Starting preview

Start the HyperFrames preview server with hot reload:

```bash
npx hyperframes preview
```

## Lint and validate before rendering

Run in this order for fastest feedback loop:

```bash
npx hyperframes lint composition.html      # structural issues
npx hyperframes validate composition.html  # runtime issues (missing assets, JS errors)
```

## Optional: single-frame render check

Render one frame to sanity-check layout, colors, or timing.
Skip for trivial edits or when you already have confidence from preview.

```bash
npx hyperframes render --frame 30 --output check.png
```

## Full render

Render the full video to MP4:

```bash
npx hyperframes render --output output.mp4
```

## How to use

Read individual rule files for detailed explanations and code examples:

- [rules/composition.md](rules/composition.md) - Composition structure, root element, data attributes
- [rules/timing.md](rules/timing.md) - Timing with data-start, data-duration, data-track-index
- [rules/animations.md](rules/animations.md) - GSAP animations, easing, timelines, exit anims, sequences
- [rules/transitions.md](rules/transitions.md) - Scene transitions and catalog transition blocks
- [rules/sequencing.md](rules/sequencing.md) - Sequencing clips and layering tracks
- [rules/video.md](rules/video.md) - Embedding video clips in compositions
- [rules/audio.md](rules/audio.md) - Audio clips, volume, mixing
- [rules/images.md](rules/images.md) - Image elements in compositions
- [rules/text.md](rules/text.md) - Text elements, typography, caption overlays
- [rules/fonts.md](rules/fonts.md) - Loading Google Fonts and local fonts
- [rules/lottie.md](rules/lottie.md) - Lottie/dotLottie animations, frame-synced scrubbing
- [rules/3d.md](rules/3d.md) - 3D effects with CSS transforms and Three.js
- [rules/variables.md](rules/variables.md) - Dynamic variables for parametric compositions
- [rules/catalog.md](rules/catalog.md) - Using pre-built catalog blocks (50+ components)
- [rules/rendering.md](rules/rendering.md) - Rendering to MP4/MOV/WebM, lint, validate, CLI options
- [rules/voiceover.md](rules/voiceover.md) - AI-generated voiceover using ElevenLabs TTS
- [rules/player.md](rules/player.md) - Embedding rendered videos with @hyperframes/player
- [rules/agent-workflow.md](rules/agent-workflow.md) - AI agent workflow, prompting patterns, anti-patterns
- [rules/examples.md](rules/examples.md) - Starter templates (warm-grain, kinetic-type, product-promo, etc.)

## Requirements

- Node.js ≥ 22
- FFmpeg (required for local video encoding)
- npm or bun

## Critical rules (always apply)

- All timed elements MUST have `class="clip"` plus `data-start`, `data-duration`, `data-track-index`
- GSAP timelines MUST be initialized with `{ paused: true }` and registered on `window.__timelines`
- Video elements MUST be `muted` to ensure deterministic rendering
- Never use `Math.random()` — compositions must be deterministic
- Root element MUST have `data-composition-id`, `data-width`, and `data-height`
