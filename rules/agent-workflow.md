---
name: agent-workflow
description: AI agent workflow patterns for HyperFrames - prompting, iteration, vocabulary, anti-patterns
metadata:
  tags: agent, workflow, prompting, iteration, anti-patterns, claude-code
---

# HyperFrames AI Agent Workflow

HyperFrames is designed specifically for AI agents. This guide covers how to work with it effectively.

## Always use the slash command

Load the skill context before starting:

```
/hyperframes
```

This ensures the agent applies all composition rules correctly from the first message rather than guessing at conventions.

## Two prompt shapes

### Cold start — describe from scratch

Specify duration, aspect ratio, mood, and key elements:

```
/hyperframes Create a 12-second product ad. Landscape 1920×1080.
Dark background, bold white headline fades in at 1s, product image
slides in from right at 3s, price tag pops in at 6s, CTA button
pulses at 9s. Energetic feel with snappy easing.
```

### Warm start — transform existing content

Provide URLs, documents, or data for richer results:

```
/hyperframes Turn this CSV into a 15-second animated bar chart race.
Portrait 1080×1920. Data: [attach CSV]. Brand colors: #0066ff accent.
```

## Iteration pattern

Treat compositions like a video editor — small targeted edits, not full re-prompts:

```
Make the headline 1.5x bigger and push it 80px higher.
```

```
Add a white vignette overlay at 8s that fades in over 1s.
```

```
The product image enter animation is too slow — cut it to 0.4s.
```

Targeted edits are faster and preserve working parts of the composition.

## Natural language → framework vocabulary

Use these terms to get consistent results:

| What you say            | What it maps to                          |
|-------------------------|------------------------------------------|
| `smooth`                | `power2.out` easing                      |
| `snappy`                | `power3.out` easing                      |
| `bouncy`                | `back.out(1.7)` easing                   |
| `springy`               | `elastic.out(1, 0.5)` easing             |
| `calm transition`       | blur crossfade                           |
| `medium transition`     | push slide                               |
| `high-energy transition`| glitch or zoom-through                   |
| `hype captions`         | heavy font, scale-pop animation          |
| `corporate captions`    | clean sans-serif, fade + slide           |
| `bass-reactive`         | `data-audio-reactive="bass:scale"`       |
| `landscape`             | 1920×1080                                |
| `portrait`              | 1080×1920                                |
| `square`                | 1080×1080                                |

## Lint and validate before debugging

When something looks wrong, run these first:

```bash
# Structural issues (missing class="clip", unregistered timelines, etc.)
npx hyperframes lint composition.html

# Runtime issues (JS exceptions, missing assets, contrast problems)
npx hyperframes validate composition.html
```

Fix lint errors before trying to debug visual issues — most rendering problems are structural.

## Anti-patterns (never do these)

| Anti-pattern                                  | Why it breaks                                          |
|-----------------------------------------------|--------------------------------------------------------|
| Ask for React / Vue components                | HyperFrames is plain HTML — no framework wrappers      |
| Use `Math.random()` in the composition        | Rendering is deterministic — same input = same output  |
| Use CSS `animation:` or `transition:` for timing | Won't render correctly frame-by-frame                |
| Skip `{ paused: true }` on GSAP timelines     | Timeline plays immediately instead of at `data-start`  |
| Forget `class="clip"` on timed elements       | Element won't be tracked by the renderer               |
| Leave video elements un-muted                 | Causes non-deterministic frame capture                 |
| Build async GSAP timelines                    | Timelines must be constructed synchronously             |
| Ask agent to "generate assets" without paths  | Agent can't know what files exist — provide paths       |

## Validate the full pipeline

After creating a new composition:

```bash
# 1. Check structure
npx hyperframes lint composition.html

# 2. Preview in browser (hot reload)
npx hyperframes preview

# 3. Render a single frame to check layout
npx hyperframes render --frame 30 --output check.png

# 4. Full render
npx hyperframes render --output output.mp4
```

## Working with assets

Always provide explicit file paths. Agents cannot discover assets:

```
/hyperframes Add the product image at assets/product.png starting at 3s.
```

Never:

```
/hyperframes Add a product image
```

## Synchronous timeline construction

GSAP timelines must be constructed fully synchronously inside a `<script>` tag. Never use `setTimeout`, `fetch`, or `async/await` inside timeline setup:

```js
// CORRECT
window.__timelines = window.__timelines || {};
const tl = gsap.timeline({ paused: true });
tl.fromTo("#title", { opacity: 0 }, { opacity: 1, duration: 0.5 });
window.__timelines["title"] = tl;

// FORBIDDEN — async inside timeline setup
fetch('/data.json').then(d => {
  const tl = gsap.timeline({ paused: true });  // async: will not render correctly
  window.__timelines["title"] = tl;
});
```
