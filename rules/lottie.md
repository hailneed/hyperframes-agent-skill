---
name: lottie
description: Embedding Lottie animations as frame-synced clips in HyperFrames compositions
metadata:
  tags: lottie, dotlottie, animation, json, frame-adapter
---

## Overview

HyperFrames supports Lottie animations via the **dotLottie** web player. Lottie files play synchronized with the composition timeline using GSAP scrubbing.

## Setup

Load the dotLottie player script in `<head>`:

```html
<script src="https://unpkg.com/@dotlottie/player-component@latest/dist/dotlottie-player.js"></script>
```

## Basic Lottie clip

```html
<dotlottie-player
  id="icon-anim"
  class="clip"
  data-start="1"
  data-duration="3"
  data-track-index="2"
  src="assets/icon.lottie"
  style="width: 200px; height: 200px; position: absolute; top: 440px; left: 860px;"
  autoplay
  loop>
</dotlottie-player>
```

## Frame-synced Lottie (scrubbed by GSAP)

For deterministic frame-accurate playback, scrub the Lottie animation via GSAP instead of using `autoplay`:

```html
<dotlottie-player
  id="logo-reveal"
  class="clip"
  data-start="0.5"
  data-duration="2"
  data-track-index="3"
  src="assets/logo.lottie"
  style="width: 400px; height: 400px; position: absolute; top: 340px; left: 760px;">
</dotlottie-player>

<script>
  window.__timelines = window.__timelines || {};

  const player = document.getElementById('logo-reveal');

  // Wait for player ready, then register scrub timeline
  player.addEventListener('ready', () => {
    const tl = gsap.timeline({ paused: true });

    // Scrub from frame 0 to frame 1 (progress 0→1) over the clip duration
    tl.to(player, {
      onUpdate() {
        const progress = tl.progress();
        player.seek(progress * 100);  // seek accepts 0–100 (%)
      },
      duration: 2,
      ease: "none",
    });

    window.__timelines["logo-reveal"] = tl;
  });
</script>
```

## Lottie formats

| Format    | Extension | Notes                                       |
|-----------|-----------|---------------------------------------------|
| dotLottie | `.lottie` | Preferred — smaller, supports multiple anims |
| JSON      | `.json`   | Classic Lottie format, widely compatible    |

## Playing a specific animation from a multi-animation .lottie

```html
<dotlottie-player
  id="multi"
  class="clip"
  data-start="2"
  data-duration="4"
  data-track-index="2"
  src="assets/bundle.lottie"
  autoplay
  style="width: 300px; height: 300px; position: absolute; top: 390px; left: 810px;">
</dotlottie-player>

<script>
  const player = document.getElementById('multi');
  player.addEventListener('ready', () => {
    player.playAnimation('success-icon');  // animation ID inside the bundle
  });
</script>
```

## Stopping on the last frame

By default, Lottie loops. To freeze on the last frame:

```js
player.addEventListener('complete', () => {
  player.seek(100);  // hold at 100%
  player.pause();
});
```

## Lottie as entrance animation

Combine with GSAP to animate the container in while the Lottie plays inside:

```html
<div id="badge-wrapper"
     class="clip"
     data-start="2"
     data-duration="5"
     data-track-index="3"
     style="position: absolute; top: 380px; left: 760px; opacity: 0;">
  <dotlottie-player src="assets/badge.lottie" autoplay style="width:360px;height:360px;"></dotlottie-player>
</div>

<script>
  window.__timelines = window.__timelines || {};
  const tl = gsap.timeline({ paused: true });
  tl.fromTo("#badge-wrapper",
    { opacity: 0, scale: 0.6 },
    { opacity: 1, scale: 1, duration: 0.5, ease: "back.out(1.5)" }
  );
  window.__timelines["badge-wrapper"] = tl;
</script>
```

## Resources

- Free Lottie animations: [lottiefiles.com](https://lottiefiles.com)
- dotLottie player docs: https://developers.lottiefiles.com/docs/dotlottie-player/dotlottie-web/
