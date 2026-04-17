---
name: fonts
description: Loading Google Fonts and local fonts in HyperFrames compositions
metadata:
  tags: fonts, google-fonts, typography, custom-fonts
---

## Google Fonts

Import via `<link>` in the `<head>`. Always use `display=swap`:

```html
<head>
  <link rel="preconnect" href="https://fonts.googleapis.com"/>
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap"
        rel="stylesheet"/>
</head>
```

Then reference in CSS:

```css
font-family: 'Inter', sans-serif;
```

## Multiple weights

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;900&family=Roboto+Mono:wght@400;700&display=swap"
      rel="stylesheet"/>
```

## Local fonts

Place font files in the `assets/` directory and load with `@font-face`:

```html
<style>
  @font-face {
    font-family: 'BrandFont';
    src: url('assets/BrandFont-Bold.woff2') format('woff2'),
         url('assets/BrandFont-Bold.woff') format('woff');
    font-weight: 700;
    font-display: swap;
  }
  @font-face {
    font-family: 'BrandFont';
    src: url('assets/BrandFont-Regular.woff2') format('woff2');
    font-weight: 400;
    font-display: swap;
  }
</style>
```

## Font pairing recommendations

| Style       | Heading font        | Body font          |
|-------------|---------------------|--------------------|
| Modern      | Inter               | Inter              |
| Editorial   | Playfair Display    | Lato               |
| Tech        | Space Grotesk       | Roboto Mono        |
| Bold/Hype   | Oswald              | Open Sans          |
| Minimal     | DM Sans             | DM Sans            |

## Variable fonts

Variable fonts give fine-grained weight control with a single file:

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap"
      rel="stylesheet"/>
```

```css
font-weight: 350; /* any value between 100–900 */
```
