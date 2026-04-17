---
name: sequencing
description: Sequencing clips, layering tracks, and building multi-scene timelines in HyperFrames
metadata:
  tags: sequencing, layering, tracks, scenes, timeline, ordering
---

## Sequential clips (cut editing)

Place clips end-to-end by setting `data-start` of each clip to the end of the previous:

```html
<!-- Scene 1: 0s–5s -->
<video id="s1" class="clip" data-start="0"  data-duration="5"  data-track-index="0" src="s1.mp4" muted></video>
<!-- Scene 2: 5s–12s -->
<video id="s2" class="clip" data-start="5"  data-duration="7"  data-track-index="0" src="s2.mp4" muted></video>
<!-- Scene 3: 12s–18s -->
<video id="s3" class="clip" data-start="12" data-duration="6"  data-track-index="0" src="s3.mp4" muted></video>
```

## Track layering

Higher `data-track-index` renders on top. Organize by purpose:

| Track index | Purpose                    |
|-------------|----------------------------|
| 0           | Background / base video    |
| 1           | Secondary video / B-roll   |
| 2           | Images / graphics          |
| 3           | Text / headlines           |
| 4           | Overlays / transitions     |
| 5+          | Captions / UI elements     |
| 9–11        | Audio tracks               |

## Parallel clips (multi-layer)

Multiple clips with the same time range but different `data-track-index` display simultaneously:

```html
<!-- Background video -->
<video id="bg"    class="clip" data-start="0" data-duration="10" data-track-index="0" src="bg.mp4" muted></video>
<!-- Graphic overlay -->
<img   id="logo"  class="clip" data-start="2" data-duration="7"  data-track-index="2" src="logo.png"/>
<!-- Text overlay -->
<div   id="title" class="clip" data-start="1" data-duration="8"  data-track-index="3" style="color:white;">Title</div>
<!-- Audio -->
<audio id="music" class="clip" data-start="0" data-duration="10" data-track-index="9" src="bg.mp3"></audio>
```

## Delayed start (hold)

To delay a clip, simply set a later `data-start`. The clip is invisible until its start time:

```html
<!-- Appears after 3 seconds -->
<div id="cta"
     class="clip"
     data-start="3"
     data-duration="7"
     data-track-index="3"
     style="...">
  Click here!
</div>
```

## Trim duration (limit clip length)

To cut a clip short, set `data-duration` to the desired visible length.  
For video content, also use `data-clip-in` / `data-clip-out` to select the source segment — see [video.md](./video.md).

## Scene builder pattern

Organize large compositions by grouping scene clips inside named `<div>` containers (purely visual, no effect on rendering):

```html
<!-- === SCENE 1: Intro === -->
<video id="s1-bg"    class="clip" data-start="0" data-duration="8" data-track-index="0" src="intro.mp4" muted></video>
<div   id="s1-title" class="clip" data-start="1" data-duration="6" data-track-index="3" style="color:white;">Intro</div>

<!-- === SCENE 2: Product === -->
<video id="s2-bg"    class="clip" data-start="8"  data-duration="10" data-track-index="0" src="product.mp4" muted></video>
<img   id="s2-logo"  class="clip" data-start="9"  data-duration="8"  data-track-index="2" src="logo.png"/>
<div   id="s2-title" class="clip" data-start="10" data-duration="6"  data-track-index="3" style="color:white;">Product</div>

<!-- === SCENE 3: CTA === -->
<video id="s3-bg"    class="clip" data-start="18" data-duration="7" data-track-index="0" src="cta.mp4" muted></video>
<div   id="s3-cta"   class="clip" data-start="19" data-duration="5" data-track-index="3" style="color:white;">Buy Now</div>
```
