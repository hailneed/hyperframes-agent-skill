# hyperframes-skill

Agent skill for [HyperFrames](https://github.com/heygen-com/hyperframes) — Write HTML. Render video. Built for agents.

Teaches AI agents (Claude Code, Cursor, Codex, etc.) the domain-specific patterns, rules, and best practices needed to generate correct HyperFrames compositions on the first attempt.

## Install

```bash
npx skills add YOUR_USERNAME/hyperframes-skill
```

## What's included

| Rule file | Covers |
|---|---|
| `composition` | HTML structure, root element, required `data-*` attributes |
| `timing` | `data-start`, `data-duration`, `data-track-index`, frame math |
| `animations` | GSAP timelines, easing, exit animations, multi-step sequences |
| `transitions` | Crossfades, wipes, 13+ catalog shader transitions |
| `sequencing` | Track layering, scene builder pattern |
| `video` | Video clips, `muted`, trimming, PiP, transparent video |
| `audio` | Audio mixing, volume, fades |
| `images` | Image overlays, formats |
| `text` | Typography, lower thirds, typewriter, captions |
| `fonts` | Google Fonts, local fonts, variable fonts |
| `lottie` | dotLottie animations, GSAP frame-synced scrubbing |
| `3d` | CSS 3D transforms, Three.js GSAP-driven render loop |
| `variables` | Dynamic variables, batch rendering |
| `catalog` | 50+ pre-built blocks (social overlays, charts, 3D effects) |
| `rendering` | CLI options, lint → validate → preview → render pipeline |
| `voiceover` | ElevenLabs TTS integration, duration-based timing |
| `player` | `@hyperframes/player` web component embedding |
| `agent-workflow` | Prompt patterns, anti-patterns, iteration, vocabulary |
| `examples` | 9 starter templates with use-case guide |

## Requirements

- Node.js ≥ 22
- FFmpeg

## Related

- [HyperFrames](https://github.com/heygen-com/hyperframes)
- [HyperFrames Docs](https://hyperframes.heygen.com)
- [Catalog](https://hyperframes.heygen.com/catalog)
