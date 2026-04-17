---
name: player
description: Embedding HyperFrames compositions in websites and apps with @hyperframes/player
metadata:
  tags: player, embed, web-component, playback, react, vue
---

## Overview

`@hyperframes/player` is a 3KB web component for embedding rendered HyperFrames compositions in any website, dashboard, or app. It mirrors the native `<video>` element API.

## Installation

```bash
npm install @hyperframes/player
```

Or via CDN (no build step):

```html
<script src="https://cdn.jsdelivr.net/npm/@hyperframes/player"></script>
```

## Basic embed

```html
<hyperframes-player
  src="output.mp4"
  controls
  autoplay
  muted>
</hyperframes-player>
```

## Attributes

| Attribute       | Type    | Default  | Description                                          |
|-----------------|---------|----------|------------------------------------------------------|
| `src`           | string  | —        | Path or URL to rendered MP4/WebM                     |
| `controls`      | boolean | false    | Show playback controls                               |
| `autoplay`      | boolean | false    | Start playing when ready                             |
| `muted`         | boolean | false    | Mute audio (required for `autoplay` in most browsers)|
| `loop`          | boolean | false    | Loop playback                                        |
| `poster`        | string  | —        | Thumbnail image URL shown before play                |
| `playback-rate` | number  | 1        | Playback speed multiplier                            |

## JavaScript API

```js
const player = document.querySelector('hyperframes-player');

// Control playback
player.play();
player.pause();
player.seek(5.0);       // jump to 5 seconds

// Read state
console.log(player.currentTime);  // current position in seconds
console.log(player.duration);     // total duration
console.log(player.paused);       // boolean
```

## Events

```js
const player = document.querySelector('hyperframes-player');

player.addEventListener('ready',      () => console.log('loaded'));
player.addEventListener('play',       () => console.log('playing'));
player.addEventListener('pause',      () => console.log('paused'));
player.addEventListener('ended',      () => console.log('finished'));
player.addEventListener('timeupdate', (e) => console.log('time:', e.detail.currentTime));
player.addEventListener('error',      (e) => console.error(e.detail));
```

## Responsive sizing

The player scales to fill its container while maintaining aspect ratio:

```html
<div style="max-width: 960px; margin: 0 auto;">
  <hyperframes-player
    src="ad.mp4"
    controls
    style="width: 100%; aspect-ratio: 16/9;">
  </hyperframes-player>
</div>
```

## React integration

```jsx
import '@hyperframes/player';

export function VideoEmbed({ src }) {
  return (
    <hyperframes-player
      src={src}
      controls
      muted
      style={{ width: '100%', aspectRatio: '16/9' }}
    />
  );
}
```

## Vue integration

```vue
<template>
  <hyperframes-player
    :src="videoSrc"
    controls
    muted
    style="width: 100%; aspect-ratio: 16/9;"
    @ended="onEnded"
  />
</template>

<script setup>
import '@hyperframes/player';
const videoSrc = 'output.mp4';
const onEnded = () => console.log('done');
</script>
```

## When to use vs. native `<video>`

| Scenario                                   | Use                      |
|--------------------------------------------|--------------------------|
| Embed a rendered MP4/WebM                  | `<hyperframes-player>`   |
| Need custom event hooks for the composition| `<hyperframes-player>`   |
| Maximum browser compatibility for video    | Native `<video>`         |
| Embedding inside another HyperFrames comp  | `<iframe>` clip          |
