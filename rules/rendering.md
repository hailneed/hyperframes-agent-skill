---
name: rendering
description: Rendering HyperFrames compositions to MP4/MOV/WebM with CLI options
metadata:
  tags: rendering, cli, mp4, mov, webm, output, quality, fps
---

## Basic render

```bash
npx hyperframes render --output output.mp4
```

## Render a specific composition file

```bash
npx hyperframes render composition.html --output output.mp4
```

## Output formats

| Format | Command                                        |
|--------|------------------------------------------------|
| MP4    | `npx hyperframes render --output output.mp4`   |
| MOV    | `npx hyperframes render --output output.mov`   |
| WebM   | `npx hyperframes render --output output.webm`  |

## Quality and scale

```bash
# Half resolution (faster, good for drafts)
npx hyperframes render --scale 0.5 --output draft.mp4

# Full quality
npx hyperframes render --quality high --output final.mp4

# Custom CRF (lower = higher quality, larger file)
npx hyperframes render --crf 18 --output hq.mp4
```

## Frame rate

```bash
# 24fps cinematic
npx hyperframes render --fps 24 --output cinematic.mp4

# 60fps smooth
npx hyperframes render --fps 60 --output smooth.mp4
```

## Single frame render (layout check)

Render one frame to verify layout before full render:

```bash
npx hyperframes render --frames 1 --output frame-check.png
```

Render a specific frame (e.g., frame 90 = 3 seconds at 30fps):

```bash
npx hyperframes render --frame 90 --output frame-90.png
```

## Render with variable overrides

```bash
npx hyperframes render \
  --vars '{"headline":"Summer Sale","accent":"#ff6600"}' \
  --output summer-sale.mp4
```

## Docker render (reproducible)

For CI/CD pipelines, use the Docker image for guaranteed identical output:

```bash
docker run --rm \
  -v "$(pwd):/project" \
  ghcr.io/heygen-com/hyperframes:latest \
  render /project/composition.html --output /project/output.mp4
```

## Preview before render

Always preview first to catch issues without waiting for a full render:

```bash
npx hyperframes preview
```

The preview server hot-reloads on HTML changes and allows scrubbing the timeline.

## Lint before render

Check for structural errors:

```bash
npx hyperframes lint composition.html
```

Common lint errors:
- Missing `class="clip"` on timed elements
- GSAP timeline not registered on `window.__timelines`
- Video element missing `muted` attribute
- `Math.random()` usage (non-deterministic)
- Root element missing `data-composition-id`

## Validate runtime behavior

After linting, validate for runtime issues (JS exceptions, missing assets, color contrast):

```bash
npx hyperframes validate composition.html
```

Run in this order: `lint` → `validate` → `preview` → `render`.
