---
name: images
description: Image elements in HyperFrames compositions
metadata:
  tags: images, img, overlay, logo, background
---

## Basic image clip

```html
<img id="logo"
     class="clip"
     data-start="2"
     data-duration="8"
     data-track-index="3"
     src="logo.png"
     style="width: 200px; height: auto; top: 40px; right: 60px; position: absolute;"/>
```

## Full-screen background image

```html
<img id="bg"
     class="clip"
     data-start="0"
     data-duration="10"
     data-track-index="0"
     src="background.jpg"
     style="width: 1920px; height: 1080px; object-fit: cover; position: absolute; top: 0; left: 0;"/>
```

## Image with GSAP fade-in

```html
<img id="product"
     class="clip"
     data-start="1"
     data-duration="9"
     data-track-index="2"
     src="product.png"
     style="width: 600px; position: absolute; top: 240px; left: 660px;"/>

<script>
  window.__timelines = window.__timelines || {};
  const tl = gsap.timeline({ paused: true });
  tl.fromTo("#product",
    { opacity: 0, scale: 0.9 },
    { opacity: 1, scale: 1, duration: 0.7, ease: "power2.out" }
  );
  window.__timelines["product"] = tl;
</script>
```

## Circular avatar / thumbnail

```html
<img id="avatar"
     class="clip"
     data-start="0"
     data-duration="15"
     data-track-index="2"
     src="profile.jpg"
     style="width: 120px; height: 120px; border-radius: 50%; object-fit: cover;
            position: absolute; bottom: 80px; left: 80px;"/>
```

## Supported formats

- PNG (with transparency)
- JPG / JPEG
- WebP
- GIF (first frame only — for animated GIFs use a `<video>` element with a looping WebM)
- SVG
