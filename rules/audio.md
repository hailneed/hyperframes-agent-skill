---
name: audio
description: Audio clips, volume, mixing, and delay in HyperFrames compositions
metadata:
  tags: audio, sound, music, volume, mixing, voiceover
---

## Basic audio clip

```html
<audio id="bg-music"
       class="clip"
       data-start="0"
       data-duration="30"
       data-track-index="2"
       src="music.mp3"></audio>
```

## Volume control

Use `data-volume` with a value between `0` and `1`:

```html
<audio id="bg-music"
       class="clip"
       data-start="0"
       data-duration="30"
       data-track-index="2"
       data-volume="0.3"
       src="music.mp3"></audio>
```

## Mixing multiple audio tracks

Different `data-track-index` values — audio elements do not visually stack, so track index only matters for ordering in the timeline inspector:

```html
<!-- Voiceover at full volume -->
<audio id="vo"
       class="clip"
       data-start="1"
       data-duration="20"
       data-track-index="10"
       data-volume="1.0"
       src="voiceover.mp3"></audio>

<!-- Background music ducked -->
<audio id="music"
       class="clip"
       data-start="0"
       data-duration="25"
       data-track-index="9"
       data-volume="0.15"
       src="background.mp3"></audio>

<!-- Sound effect -->
<audio id="sfx"
       class="clip"
       data-start="5"
       data-duration="2"
       data-track-index="11"
       data-volume="0.8"
       src="whoosh.mp3"></audio>
```

## Trimming audio (clip-in)

Start the audio from an offset within the source file:

```html
<audio id="music-trimmed"
       class="clip"
       data-start="0"
       data-duration="15"
       data-track-index="9"
       data-clip-in="30"
       src="long-track.mp3"></audio>
```

## Fade in / fade out

Use GSAP to animate volume on an audio element via the WebAudio API, or use CSS-driven volume fades with `data-fade-in` / `data-fade-out`:

```html
<audio id="music"
       class="clip"
       data-start="0"
       data-duration="20"
       data-track-index="9"
       data-volume="0.4"
       data-fade-in="2"
       data-fade-out="3"
       src="music.mp3"></audio>
```

`data-fade-in` — duration of volume fade-in at clip start (seconds)  
`data-fade-out` — duration of volume fade-out before clip end (seconds)

## Audio-only composition

For podcasts or music visualizers with no video background, set a solid-color stage:

```html
<div id="stage"
     data-composition-id="podcast"
     data-width="1920"
     data-height="1080"
     style="background: #111;">

  <audio id="episode"
         class="clip"
         data-start="0"
         data-duration="120"
         data-track-index="0"
         src="episode.mp3"></audio>

</div>
```
