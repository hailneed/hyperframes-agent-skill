---
name: timing
description: Timing model in HyperFrames - data-start, data-duration, data-track-index, and frame math
metadata:
  tags: timing, data-start, data-duration, data-track-index, frames, fps
---

## Time unit

All timing attributes use **seconds** (floats). HyperFrames renders at 30 fps by default.

Frame formula: `frame = floor(time * fps)`

| Seconds | Frames (30fps) |
|---------|---------------|
| 0.0     | 0             |
| 1.0     | 30            |
| 2.5     | 75            |
| 10.0    | 300           |

## Required timing attributes

Every `.clip` element needs all three:

| Attribute          | Type    | Description                              |
|--------------------|---------|------------------------------------------|
| `data-start`       | float   | When the clip starts (seconds)           |
| `data-duration`    | float   | How long the clip plays (seconds)        |
| `data-track-index` | integer | Z-layer (0 = bottom, higher = on top)    |

```html
<!-- Appears at 2s, lasts 4s, renders above track 0 -->
<div class="clip"
     data-start="2"
     data-duration="4"
     data-track-index="1"
     style="...">
  Content
</div>
```

## Clip end time

`end = data-start + data-duration`

A clip with `data-start="3" data-duration="5"` is visible from 3s → 8s.

## Total composition duration

The composition duration equals the end time of the last clip:

```
totalDuration = max(data-start + data-duration) across all clips
```

## Overlapping clips

Multiple clips can overlap in time. Use `data-track-index` to control which one renders on top.

```html
<!-- Background video, full duration -->
<video class="clip" data-start="0" data-duration="10" data-track-index="0" src="bg.mp4" muted></video>

<!-- Overlay text, appears midway -->
<div class="clip" data-start="3" data-duration="4" data-track-index="1" style="...">
  Overlay
</div>
```

## Gap between clips

To create a pause between clips, simply set `data-start` to start after the previous clip ends:

```html
<video class="clip" data-start="0"  data-duration="3" data-track-index="0" src="a.mp4" muted></video>
<video class="clip" data-start="3.5" data-duration="3" data-track-index="0" src="b.mp4" muted></video>
```

## Custom FPS

Override FPS at the root element:

```html
<div id="stage"
     data-composition-id="my-video"
     data-width="1920"
     data-height="1080"
     data-fps="60">
```
