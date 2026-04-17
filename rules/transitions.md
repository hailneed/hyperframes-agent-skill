---
name: transitions
description: Scene transitions in HyperFrames - catalog blocks, GSAP crossfades, shader effects
metadata:
  tags: transitions, crossfade, dissolve, glitch, wipe, catalog
---

## Crossfade between two clips

Overlap the clips in time and fade out the first while fading in the second using GSAP:

```html
<!-- Scene A ends at 6s, fades out over last 1s -->
<video id="scene-a"
       class="clip"
       data-start="0"
       data-duration="6"
       data-track-index="0"
       src="scene-a.mp4"
       muted></video>

<!-- Scene B starts at 5s (1s overlap), fades in -->
<video id="scene-b"
       class="clip"
       data-start="5"
       data-duration="8"
       data-track-index="0"
       src="scene-b.mp4"
       muted
       style="opacity: 0;"></video>

<script>
  window.__timelines = window.__timelines || {};

  const tlA = gsap.timeline({ paused: true });
  tlA.to("#scene-a", { opacity: 0, duration: 1, delay: 5 });
  window.__timelines["scene-a"] = tlA;

  const tlB = gsap.timeline({ paused: true });
  tlB.to("#scene-b", { opacity: 1, duration: 1 });
  window.__timelines["scene-b"] = tlB;
</script>
```

## Wipe transition (horizontal)

```html
<div id="wipe-cover"
     class="clip"
     data-start="4"
     data-duration="1"
     data-track-index="5"
     style="position: absolute; top: 0; left: -1920px; width: 1920px; height: 1080px;
            background: #000;"></div>

<script>
  window.__timelines = window.__timelines || {};
  const tl = gsap.timeline({ paused: true });
  tl.fromTo("#wipe-cover",
    { x: -1920 },
    { x: 1920, duration: 0.6, ease: "power2.inOut" }
  );
  window.__timelines["wipe-cover"] = tl;
</script>
```

## Using catalog transition blocks

Install a catalog transition block:

```bash
npx hyperframes add dissolve-transition
```

Then embed it as an iframe clip between two scenes:

```html
<!-- Scene A -->
<video id="scene-a" class="clip" data-start="0" data-duration="6"
       data-track-index="0" src="a.mp4" muted></video>

<!-- Catalog dissolve transition, covers the cut point -->
<iframe id="transition-1"
        class="clip"
        data-start="5"
        data-duration="1"
        data-track-index="4"
        src="catalog/dissolve-transition.html"
        style="width: 1920px; height: 1080px; border: none; position: absolute; top: 0; left: 0;"></iframe>

<!-- Scene B -->
<video id="scene-b" class="clip" data-start="6" data-duration="8"
       data-track-index="0" src="b.mp4" muted></video>
```

## Available catalog shader transitions

| Block name              | Effect description                        |
|-------------------------|-------------------------------------------|
| `chromatic-aberration`  | RGB channel split glitch                  |
| `glitch`                | Digital glitch distortion                 |
| `thermal-distortion`    | Heat haze warping                         |
| `ripple-waves`          | Water ripple reveal                       |
| `vortex`                | Spinning vortex wipe                      |
| `dissolve`              | Classic opacity dissolve                  |
| `blur-crossfade`        | Smooth blur dissolve (calm feel)          |
| `push-left`             | Slide push in from right                  |
| `push-up`               | Slide push in from bottom                 |
| `scale-in`              | Zoom-in reveal                            |
| `grid-wipe`             | Grid tile reveal                          |
| `radial-wipe`           | Circular reveal from center               |
| `mechanical-wipe`       | Shutter-style mechanical wipe             |

Install any block: `npx hyperframes add <block-name>`
