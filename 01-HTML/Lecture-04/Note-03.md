# Advanced SVG Integration Notes

## 1. Inline SVG

**What it is:** Embedding SVG code directly into HTML rather than linking to external files.

**Advantages:**

- No extra HTTP requests
- Can be styled with CSS
- Can be manipulated with JavaScript
- Better for animations and interactivity

**Basic Example:**

```html
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
  <circle cx="100" cy="100" r="80" fill="#3498db" />
  <text x="100" y="110" text-anchor="middle" fill="white" font-size="24">
    SVG
  </text>
</svg>
```

**Practical Use - Icon System:**

```html
<style>
  .icon {
    width: 24px;
    height: 24px;
    fill: currentColor;
  }
  .icon:hover {
    fill: #e74c3c;
  }
</style>

<svg class="icon" viewBox="0 0 24 24">
  <path
    d="M12 2L2 7v10c0 5.55 3.84 10.74 9 12 5.16-1.26 9-6.45 9-12V7l-10-5z"
  />
</svg>
```

## 2. SVG Animation

**Methods:**

- CSS animations (most common)
- SMIL (SVG's native animation)
- JavaScript/Web Animations API

### CSS Animation Example:

```html
<svg width="300" height="300">
  <style>
    .rotating-circle {
      animation: rotate 3s linear infinite;
      transform-origin: center;
    }
    @keyframes rotate {
      from {
        transform: rotate(0deg);
      }
      to {
        transform: rotate(360deg);
      }
    }

    .pulsing {
      animation: pulse 2s ease-in-out infinite;
    }
    @keyframes pulse {
      0%,
      100% {
        r: 40;
        opacity: 1;
      }
      50% {
        r: 60;
        opacity: 0.5;
      }
    }
  </style>

  <circle
    class="rotating-circle"
    cx="150"
    cy="150"
    r="50"
    fill="none"
    stroke="#3498db"
    stroke-width="5"
  />
  <circle class="pulsing" cx="150" cy="150" r="40" fill="#e74c3c" />
</svg>
```

### Path Animation (Drawing Effect):

```html
<svg width="400" height="200">
  <style>
    .draw-path {
      stroke-dasharray: 1000;
      stroke-dashoffset: 1000;
      animation: draw 2s ease-in-out forwards;
    }
    @keyframes draw {
      to {
        stroke-dashoffset: 0;
      }
    }
  </style>

  <path
    class="draw-path"
    d="M10,100 Q200,20 390,100"
    fill="none"
    stroke="#2ecc71"
    stroke-width="4"
  />
</svg>
```

### SMIL Animation (native SVG):

```html
<svg width="200" height="200">
  <circle cx="100" cy="100" r="20" fill="#9b59b6">
    <animate
      attributeName="r"
      from="20"
      to="80"
      dur="2s"
      repeatCount="indefinite"
    />
    <animate
      attributeName="opacity"
      from="1"
      to="0"
      dur="2s"
      repeatCount="indefinite"
    />
  </circle>
</svg>
```

## 3. SVG Filters

**Common Filters:**

- feGaussianBlur (blur effect)
- feDropShadow (shadow)
- feColorMatrix (color adjustments)
- feMorphology (dilate/erode)
- feDisplacementMap (distortion)

### Blur & Glow Effect:

```html
<svg width="300" height="200">
  <defs>
    <filter id="glow">
      <feGaussianBlur stdDeviation="4" result="coloredBlur" />
      <feMerge>
        <feMergeNode in="coloredBlur" />
        <feMergeNode in="SourceGraphic" />
      </feMerge>
    </filter>
  </defs>

  <circle cx="150" cy="100" r="50" fill="#f39c12" filter="url(#glow)" />
</svg>
```

### Drop Shadow:

```html
<svg width="300" height="200">
  <defs>
    <filter id="shadow" x="-50%" y="-50%" width="200%" height="200%">
      <feDropShadow dx="4" dy="4" stdDeviation="3" flood-opacity="0.5" />
    </filter>
  </defs>

  <rect
    x="50"
    y="50"
    width="200"
    height="100"
    fill="#3498db"
    filter="url(#shadow)"
    rx="10"
  />
</svg>
```

### Duotone Effect:

```html
<svg width="400" height="300">
  <defs>
    <filter id="duotone">
      <feColorMatrix
        type="matrix"
        values="
        0.3 0.3 0.3 0 0
        0.6 0.6 0.6 0 0
        0.1 0.1 0.1 0 0
        0   0   0   1 0"
      />
    </filter>
  </defs>

  <image href="photo.jpg" width="400" height="300" filter="url(#duotone)" />
</svg>
```

### Noise/Texture Filter:

```html
<svg width="300" height="200">
  <defs>
    <filter id="noise">
      <feTurbulence
        type="fractalNoise"
        baseFrequency="0.9"
        numOctaves="4"
        result="noise"
      />
      <feBlend in="SourceGraphic" in2="noise" mode="multiply" />
    </filter>
  </defs>

  <rect width="300" height="200" fill="#e74c3c" filter="url(#noise)" />
</svg>
```

## 4. SVG Accessibility

**Key Principles:**

- Add semantic information
- Provide text alternatives
- Ensure keyboard navigation
- Use proper ARIA attributes

### Basic Accessibility:

```html
<svg
  role="img"
  aria-labelledby="chart-title chart-desc"
  width="400"
  height="300"
>
  <title id="chart-title">Sales Data 2024</title>
  <desc id="chart-desc">Bar chart showing quarterly sales from Q1 to Q4</desc>

  <rect x="50" y="100" width="60" height="150" fill="#3498db">
    <title>Q1: $50,000</title>
  </rect>
  <rect x="150" y="80" width="60" height="170" fill="#2ecc71">
    <title>Q2: $65,000</title>
  </rect>
</svg>
```

### Decorative vs Informative:

```html
<!-- Decorative (hidden from screen readers) -->
<svg aria-hidden="true" focusable="false">
  <circle cx="50" cy="50" r="40" fill="#ddd" />
</svg>

<!-- Informative (accessible) -->
<svg role="img" aria-label="Warning icon">
  <path d="M12 2L2 22h20L12 2z" />
  <text x="12" y="18" text-anchor="middle">!</text>
</svg>
```

### Interactive SVG with Accessibility:

```html
<svg width="300" height="300" role="img" aria-label="Interactive buttons">
  <g role="button" tabindex="0" aria-label="Play button">
    <circle cx="150" cy="150" r="50" fill="#2ecc71" />
    <polygon points="140,130 140,170 170,150" fill="white" />
  </g>

  <style>
    g[role="button"]:focus {
      outline: 3px solid #f39c12;
      outline-offset: 5px;
    }
    g[role="button"]:hover circle {
      fill: #27ae60;
    }
  </style>
</svg>
```

### ARIA Live Regions for Dynamic Content:

```html
<svg width="400" height="100">
  <text
    id="status"
    x="200"
    y="50"
    text-anchor="middle"
    aria-live="polite"
    role="status"
  >
    Loading...
  </text>
</svg>

<script>
  // Screen readers will announce changes
  document.getElementById("status").textContent = "Data loaded successfully";
</script>
```

### Complex Chart Accessibility:

```html
<figure>
  <figcaption>Monthly Revenue Chart</figcaption>

  <svg
    role="img"
    aria-labelledby="chart-title"
    aria-describedby="chart-summary"
    width="500"
    height="300"
  >
    <title id="chart-title">2024 Revenue Trend</title>
    <desc id="chart-summary">
      Line chart showing revenue increasing from $10K in January to $45K in
      December
    </desc>

    <!-- Chart content -->
  </svg>

  <!-- Provide data table alternative -->
  <details>
    <summary>View data table</summary>
    <table>
      <thead>
        <tr>
          <th>Month</th>
          <th>Revenue</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>January</td>
          <td>$10,000</td>
        </tr>
        <tr>
          <td>February</td>
          <td>$15,000</td>
        </tr>
      </tbody>
    </table>
  </details>
</figure>
```

## Best Practices Summary

**Inline SVG:**

- Use `viewBox` for responsive scaling
- Minimize code (remove unnecessary attributes)
- Consider using SVG sprites for multiple icons

**Animation:**

- Prefer CSS animations for performance
- Use `will-change` for complex animations
- Respect `prefers-reduced-motion`

**Filters:**

- Define filters in `<defs>` for reusability
- Be cautious with performance on complex filters
- Test across browsers

**Accessibility:**

- Always include `<title>` and `<desc>` for informative SVGs
- Use `aria-hidden="true"` for decorative SVGs
- Ensure interactive elements are keyboard accessible
- Provide alternative text representations for complex data
