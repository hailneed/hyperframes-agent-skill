---
name: composition
description: Composition structure, root element, and required data attributes in HyperFrames
metadata:
  tags: composition, html, data-attributes, root, structure
---

A HyperFrames composition is a plain HTML file. The root element defines the canvas and composition metadata.

## Root element

The root element MUST have `data-composition-id`, `data-width`, and `data-height`:

```html
<div id="stage"
     data-composition-id="my-video"
     data-width="1920"
     data-height="1080">
  <!-- clips go here -->
</div>
```

## Standard resolutions

| Format    | Width | Height |
|-----------|-------|--------|
| Landscape | 1920  | 1080   |
| Portrait  | 1080  | 1920   |
| Square    | 1080  | 1080   |

## Timed elements (clips)

Every element that has a start time and duration MUST:
- Have `class="clip"`
- Have `data-start` (seconds, float)
- Have `data-duration` (seconds, float)
- Have `data-track-index` (integer, 0 = bottom layer)

```html
<video id="clip-1"
       class="clip"
       data-start="0"
       data-duration="5"
       data-track-index="0"
       src="intro.mp4"
       muted></video>

<img id="logo"
     class="clip"
     data-start="2"
     data-duration="3"
     data-track-index="1"
     src="logo.png"/>

<audio id="bg-music"
       class="clip"
       data-start="0"
       data-duration="9"
       data-track-index="2"
       data-volume="0.5"
       src="music.wav"></audio>
```

## Minimal complete composition

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8"/>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    #stage { width: 1920px; height: 1080px; position: relative; background: #000; }
    .clip { position: absolute; }
  </style>
</head>
<body>
  <div id="stage"
       data-composition-id="intro-video"
       data-width="1920"
       data-height="1080">

    <video id="bg"
           class="clip"
           data-start="0"
           data-duration="10"
           data-track-index="0"
           src="background.mp4"
           muted></video>

    <div id="title"
         class="clip"
         data-start="1"
         data-duration="8"
         data-track-index="1"
         style="color: white; font-size: 80px; top: 440px; left: 760px;">
      Hello World
    </div>

  </div>
</body>
</html>
```

## Nesting compositions

Embed a sub-composition using an `<iframe>` clip:

```html
<iframe id="lower-third"
        class="clip"
        data-start="3"
        data-duration="5"
        data-track-index="2"
        src="lower-third.html"
        style="width: 1920px; height: 200px; top: 880px; border: none;"></iframe>
```
