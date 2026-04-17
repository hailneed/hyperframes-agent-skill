---
name: catalog
description: Using pre-built HyperFrames catalog blocks - social overlays, charts, transitions, 3D effects
metadata:
  tags: catalog, blocks, components, social, overlays, charts, transitions
---

HyperFrames ships 50+ ready-to-use blocks. Install any block and embed it as an `<iframe>` clip.

## Installing a catalog block

```bash
npx hyperframes add <block-name>
```

The block is added to the `catalog/` directory in your project.

## Embedding a block

All catalog blocks are embedded as `<iframe>` clips:

```html
<iframe id="spotify-card"
        class="clip"
        data-start="2"
        data-duration="5"
        data-track-index="3"
        src="catalog/spotify-now-playing.html"
        style="width: 480px; height: 120px; border: none; position: absolute; bottom: 60px; left: 60px;"></iframe>
```

## Social overlay blocks

| Block name              | Description                                        |
|-------------------------|----------------------------------------------------|
| `instagram-follow`      | Animated Instagram follow card with profile photo  |
| `tiktok-follow`         | TikTok follow overlay with like/comment counts     |
| `spotify-now-playing`   | Spotify-style now-playing card with album art      |
| `youtube-lower-third`   | YouTube-style name lower third                     |
| `reddit-post`           | Reddit post card overlay                           |
| `x-post`                | X (Twitter) post card overlay                      |
| `macos-notification`    | macOS-style notification banner                    |

## Installing social blocks

```bash
npx hyperframes add instagram-follow
npx hyperframes add tiktok-follow
npx hyperframes add spotify-now-playing
npx hyperframes add youtube-lower-third
```

## Data visualization blocks

| Block name              | Description                                        |
|-------------------------|----------------------------------------------------|
| `bar-chart`             | Animated bar chart with staggered reveal           |
| `line-chart`            | Animated line/area chart                           |
| `pie-chart`             | Animated donut/pie chart                           |
| `stat-counter`          | Large animated number counter                      |

Pass data to chart blocks via URL query parameters or `data-var-*` attributes.

## 3D effect blocks

| Block name              | Description                                        |
|-------------------------|----------------------------------------------------|
| `perspective-reveal`    | 3D card perspective flip reveal                    |
| `flip-transition`       | 3D page flip transition                            |

## Passing data to blocks

Blocks that accept data use URL hash or query string:

```html
<iframe id="bar-chart"
        class="clip"
        data-start="3"
        data-duration="6"
        data-track-index="3"
        src="catalog/bar-chart.html?labels=Q1,Q2,Q3,Q4&values=120,240,180,310&color=%23ff3c00"
        style="width: 800px; height: 500px; border: none; position: absolute;
               top: 290px; left: 560px;"></iframe>
```

## Browsing all blocks

```bash
npx hyperframes catalog
```

Or visit: https://hyperframes.heygen.com/catalog
