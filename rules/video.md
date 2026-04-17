---
name: video
description: Embedding video clips in HyperFrames compositions - muted, looping, trimming, volume
metadata:
  tags: video, clip, muted, loop, trim, src
---

## Basic video clip

Video elements MUST be `muted`. Un-muted video will cause non-deterministic rendering.

```html
<video id="intro"
       class="clip"
       data-start="0"
       data-duration="8"
       data-track-index="0"
       src="intro.mp4"
       muted></video>
```

Use CSS to size and position the video within the composition canvas:

```html
<video id="bg"
       class="clip"
       data-start="0"
       data-duration="10"
       data-track-index="0"
       src="background.mp4"
       muted
       style="width: 1920px; height: 1080px; object-fit: cover;"></video>
```

## Looping video

```html
<video id="loop-bg"
       class="clip"
       data-start="0"
       data-duration="30"
       data-track-index="0"
       src="loop.mp4"
       muted
       loop></video>
```

## Trimming (clip-in / clip-out)

Use `data-clip-in` and `data-clip-out` to trim the source video (in seconds):

```html
<!-- Play only seconds 5–15 of the source video -->
<video id="trimmed"
       class="clip"
       data-start="0"
       data-duration="10"
       data-track-index="0"
       data-clip-in="5"
       data-clip-out="15"
       src="raw-footage.mp4"
       muted></video>
```

## Playback speed

```html
<video id="fast"
       class="clip"
       data-start="0"
       data-duration="5"
       data-track-index="0"
       data-playback-rate="2"
       src="clip.mp4"
       muted></video>
```

## Picture-in-picture

Place a smaller video on top of a background using `data-track-index` and CSS positioning:

```html
<!-- Full-screen background -->
<video id="main"
       class="clip"
       data-start="0"
       data-duration="15"
       data-track-index="0"
       src="main.mp4"
       muted
       style="width: 1920px; height: 1080px; object-fit: cover;"></video>

<!-- PiP overlay, bottom-right corner -->
<video id="pip"
       class="clip"
       data-start="3"
       data-duration="10"
       data-track-index="1"
       src="facecam.mp4"
       muted
       style="width: 320px; height: 180px; bottom: 40px; right: 40px; border-radius: 12px;"></video>
```

## Transparent video (alpha channel)

Use WebM with alpha for transparent video overlays:

```html
<video id="confetti"
       class="clip"
       data-start="5"
       data-duration="3"
       data-track-index="3"
       src="confetti-alpha.webm"
       muted
       style="width: 1920px; height: 1080px;"></video>
```
