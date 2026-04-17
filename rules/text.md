---
name: text
description: Text elements, typography, and caption overlays in HyperFrames
metadata:
  tags: text, typography, captions, subtitles, headline, lower-third
---

## Basic text clip

```html
<div id="headline"
     class="clip"
     data-start="1"
     data-duration="8"
     data-track-index="2"
     style="position: absolute; top: 420px; left: 0; width: 1920px;
            text-align: center; color: white; font-size: 96px;
            font-family: 'Inter', sans-serif; font-weight: 700;">
  Your Headline Here
</div>
```

## Animated text (slide up + fade)

```html
<div id="title"
     class="clip"
     data-start="0.5"
     data-duration="9"
     data-track-index="3"
     style="position: absolute; top: 380px; width: 1920px; text-align: center;
            color: #fff; font-size: 80px; font-weight: 800; opacity: 0;">
  Big Bold Title
</div>

<script>
  window.__timelines = window.__timelines || {};
  const tl = gsap.timeline({ paused: true });
  tl.to("#title", { opacity: 1, y: 0, duration: 0.7, ease: "power3.out",
                    from: { y: 50, opacity: 0 } });
  window.__timelines["title"] = tl;
</script>
```

## Word-by-word animation

Split text into `<span>` elements and stagger them:

```html
<div id="words"
     class="clip"
     data-start="1"
     data-duration="6"
     data-track-index="3"
     style="position: absolute; top: 460px; width: 1920px; text-align: center;
            color: #fff; font-size: 72px; font-weight: 700;">
  <span class="word" style="display: inline-block; opacity: 0;">Write</span>
  <span class="word" style="display: inline-block; opacity: 0; margin: 0 16px;">HTML.</span>
  <span class="word" style="display: inline-block; opacity: 0;">Render</span>
  <span class="word" style="display: inline-block; opacity: 0; margin: 0 16px;">video.</span>
</div>

<script>
  window.__timelines = window.__timelines || {};
  const tl = gsap.timeline({ paused: true });
  tl.fromTo(".word",
    { opacity: 0, y: 20 },
    { opacity: 1, y: 0, duration: 0.4, stagger: 0.15, ease: "power2.out" }
  );
  window.__timelines["words"] = tl;
</script>
```

## Lower third

```html
<div id="lower-third"
     class="clip"
     data-start="2"
     data-duration="5"
     data-track-index="4"
     style="position: absolute; bottom: 120px; left: 80px;
            background: rgba(0,0,0,0.75); padding: 16px 28px;
            border-left: 6px solid #ff3c3c; opacity: 0;">
  <div style="color: #fff; font-size: 32px; font-weight: 700; font-family: Inter, sans-serif;">
    Jane Doe
  </div>
  <div style="color: #ccc; font-size: 22px; font-family: Inter, sans-serif;">
    CEO, Acme Corp
  </div>
</div>

<script>
  window.__timelines = window.__timelines || {};
  const tl = gsap.timeline({ paused: true });
  tl.fromTo("#lower-third",
    { opacity: 0, x: -40 },
    { opacity: 1, x: 0, duration: 0.5, ease: "power2.out" }
  );
  window.__timelines["lower-third"] = tl;
</script>
```

## Typewriter effect

```html
<div id="typewriter"
     class="clip"
     data-start="1"
     data-duration="8"
     data-track-index="3"
     style="position: absolute; top: 480px; left: 200px;
            color: #fff; font-size: 60px; font-family: monospace; white-space: nowrap;
            overflow: hidden; width: 0;">
  Build videos with HTML.
</div>

<script>
  window.__timelines = window.__timelines || {};
  const tl = gsap.timeline({ paused: true });
  tl.to("#typewriter", { width: "1520px", duration: 3, ease: "steps(24)" });
  window.__timelines["typewriter"] = tl;
</script>
```

## Caption overlay (subtitles)

For time-synced captions, use separate `.clip` elements per line:

```html
<div id="caption-1"
     class="clip"
     data-start="1.2"
     data-duration="2.4"
     data-track-index="5"
     style="position: absolute; bottom: 80px; width: 1920px; text-align: center;
            color: #fff; font-size: 52px; font-family: Inter, sans-serif;
            text-shadow: 0 2px 8px rgba(0,0,0,0.8);">
  Welcome to the show.
</div>

<div id="caption-2"
     class="clip"
     data-start="3.8"
     data-duration="2.6"
     data-track-index="5"
     style="position: absolute; bottom: 80px; width: 1920px; text-align: center;
            color: #fff; font-size: 52px; font-family: Inter, sans-serif;
            text-shadow: 0 2px 8px rgba(0,0,0,0.8);">
  Today we cover everything.
</div>
```
