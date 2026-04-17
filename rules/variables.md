---
name: variables
description: Dynamic variables for parametric HyperFrames compositions
metadata:
  tags: variables, parameters, dynamic, template, data-driven
---

Variables make compositions reusable — render the same template with different data.

## Declaring variables

Define variables on the root `#stage` element using `data-var-*` attributes:

```html
<div id="stage"
     data-composition-id="product-ad"
     data-width="1920"
     data-height="1080"
     data-var-product-name="AirMax Pro"
     data-var-price="$129"
     data-var-accent-color="#ff3c00">
```

## Supported variable types

| Type    | Example value              |
|---------|----------------------------|
| string  | `"Hello World"`            |
| number  | `"42"` or `"3.14"`         |
| color   | `"#ff3c00"` or `"red"`     |
| boolean | `"true"` or `"false"`      |
| enum    | `"landscape"` or `"portrait"` |

## Reading variables in the composition

Use a small script to read `data-var-*` attributes and apply them:

```html
<script>
  const stage = document.getElementById('stage');
  const vars = {};
  for (const attr of stage.attributes) {
    if (attr.name.startsWith('data-var-')) {
      const key = attr.name.replace('data-var-', '').replace(/-([a-z])/g, (_, c) => c.toUpperCase());
      vars[key] = attr.value;
    }
  }

  // Apply variables
  document.getElementById('product-name').textContent = vars.productName;
  document.getElementById('price-tag').textContent = vars.price;
  document.documentElement.style.setProperty('--accent', vars.accentColor);
</script>
```

## CSS custom properties from variables

```html
<style>
  :root { --accent: #ff3c00; }
  .cta-button { background: var(--accent); }
</style>
```

## Rendering with custom variables via CLI

Pass variables as JSON on the command line:

```bash
npx hyperframes render \
  --vars '{"productName":"ProX","price":"$199","accentColor":"#0066ff"}' \
  --output output-prox.mp4
```

## Batch rendering

Generate multiple outputs from one template by looping:

```bash
node << 'EOF'
const { execSync } = require('child_process');
const products = [
  { productName: "AirMax Pro", price: "$129", accentColor: "#ff3c00" },
  { productName: "SpeedFit X", price: "$89",  accentColor: "#00c4ff" },
  { productName: "TrailBlazer", price: "$159", accentColor: "#22c55e" },
];
for (const p of products) {
  execSync(`npx hyperframes render --vars '${JSON.stringify(p)}' --output dist/${p.productName.replace(/ /g,'-')}.mp4`);
}
EOF
```
