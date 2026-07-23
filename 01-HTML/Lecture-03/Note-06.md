# Performance Optimization: The Essential Guide

## 1. Resource Hints

### Preload - Load Critical Resources Early

```html
<!-- Load font needed for initial render -->
<link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin />

<!-- Load critical CSS -->
<link rel="preload" href="critical.css" as="style" />

<!-- Load hero image -->
<link rel="preload" href="hero.jpg" as="image" />
```

**When to use:** Resources you KNOW you'll need immediately.

**`as` attribute values:** `font`, `style`, `script`, `image`, `fetch`, `document`

---

### Prefetch - Load for Next Navigation

```html
<!-- User likely to visit this page next -->
<link rel="prefetch" href="/next-page.html" />

<!-- Prefetch data for next page -->
<link rel="prefetch" href="/api/data.json" as="fetch" />
```

**When to use:** Resources for likely next navigation (low priority).

---

### DNS-Prefetch - Resolve DNS Early

```html
<!-- Resolve DNS before making request -->
<link rel="dns-prefetch" href="https://api.example.com" />
<link rel="dns-prefetch" href="https://cdn.example.com" />
```

**When to use:** Third-party domains you'll request from.

---

### Preconnect - Establish Connection Early

```html
<!-- DNS + TCP + TLS handshake -->
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://api.stripe.com" />
```

**When to use:** Critical third-party origins (stronger than dns-prefetch).

---

### Resource Hints Summary

| Hint           | Use Case                            | Priority |
| -------------- | ----------------------------------- | -------- |
| `preload`      | Critical resources for current page | High     |
| `prefetch`     | Resources for next navigation       | Low      |
| `dns-prefetch` | Resolve DNS early                   | Low      |
| `preconnect`   | Full connection setup               | Medium   |

**Rule:** Preload = now, Prefetch = later.

---

## 2. Lazy Loading

### Images

```html
<!-- Load only when near viewport -->
<img src="image.jpg" loading="lazy" alt="Description" />

<!-- Load immediately (default) -->
<img src="hero.jpg" loading="eager" alt="Hero" />

<!-- Browser decides -->
<img src="image.jpg" loading="auto" alt="Description" />
```

**Impact:** Saves bandwidth, faster initial load.

---

### Iframes

```html
<!-- Lazy load embedded content -->
<iframe src="https://youtube.com/embed/..." loading="lazy"></iframe>
<iframe src="map.html" loading="lazy"></iframe>
```

**Use case:** Videos, maps, ads below the fold.

---

### When NOT to Lazy Load

```html
<!-- ❌ Don't lazy load above-the-fold content -->
<img src="hero.jpg" loading="lazy" />
<!-- BAD: Delays visible content -->

<!-- ✅ Load hero immediately -->
<img src="hero.jpg" loading="eager" />
```

---

## 3. Script Loading: Async vs Defer

### Default (Blocking)

```html
<script src="app.js"></script>
```

1. HTML parsing stops
2. Script downloads
3. Script executes
4. HTML parsing resumes

**Problem:** Blocks rendering.

---

### Defer - Execute After Parsing

```html
<script src="app.js" defer></script>
```

1. HTML parsing continues
2. Script downloads in parallel
3. Script executes after HTML parsed
4. Maintains order (multiple defer scripts run in order)

**Use case:** Scripts that need full DOM access.

---

### Async - Execute ASAP

```html
<script src="analytics.js" async></script>
```

1. HTML parsing continues
2. Script downloads in parallel
3. Script executes immediately when ready (pauses parsing)
4. No order guarantee (multiple async scripts run whenever ready)

**Use case:** Independent scripts (analytics, ads).

---

### Comparison

```html
<!-- Blocks parsing -->
<script src="blocking.js"></script>

<!-- Downloads in parallel, executes after parse, in order -->
<script src="app.js" defer></script>
<script src="vendor.js" defer></script>

<!-- Downloads in parallel, executes ASAP, any order -->
<script src="analytics.js" async></script>
```

| Attribute | Downloads   | Executes    | Blocks Parsing | Order      |
| --------- | ----------- | ----------- | -------------- | ---------- |
| None      | Immediately | Immediately | ✅ Yes         | Sequential |
| `defer`   | Parallel    | After parse | ❌ No          | Sequential |
| `async`   | Parallel    | When ready  | ⚠️ Briefly     | Random     |

**Rule:** Use `defer` for your app scripts, `async` for independent third-party scripts.

---

### Module Scripts

```html
<!-- Defer by default -->
<script type="module" src="app.js"></script>

<!-- Async module -->
<script type="module" src="analytics.js" async></script>
```

**Key:** Module scripts are automatically deferred.

---

## 4. Critical Rendering Path

### The Problem

Browser must:

1. Parse HTML → Build DOM
2. Parse CSS → Build CSSOM
3. Combine DOM + CSSOM → Render Tree
4. Layout → Calculate positions
5. Paint → Draw pixels

**Blocking resources slow this down.**

---

### Optimize Critical Path

#### 1. Inline Critical CSS

```html
<head>
  <style>
    /* Critical above-the-fold styles */
    body {
      margin: 0;
      font-family: sans-serif;
    }
    .header {
      background: #333;
      color: white;
    }
  </style>

  <!-- Load full CSS async -->
  <link
    rel="preload"
    href="styles.css"
    as="style"
    onload="this.onload=null;this.rel='stylesheet'"
  />
</head>
```

---

#### 2. Defer Non-Critical CSS

```html
<!-- Load print styles async -->
<link rel="stylesheet" href="print.css" media="print" />

<!-- Load when screen is wide -->
<link rel="stylesheet" href="desktop.css" media="(min-width: 1024px)" />
```

---

#### 3. Optimize JavaScript Loading

```html
<head>
  <!-- Preload critical scripts -->
  <link rel="preload" href="critical.js" as="script" />

  <!-- Defer non-critical -->
  <script src="app.js" defer></script>

  <!-- Async third-party -->
  <script src="analytics.js" async></script>
</head>
```

---

#### 4. Reduce Parser Blocking

```html
<!-- ❌ Bad: Blocks parser -->
<head>
  <script src="large-library.js"></script>
</head>

<!-- ✅ Good: Doesn't block -->
<head>
  <script src="large-library.js" defer></script>
</head>
```

---

### Critical Rendering Path Strategy

**Priority order:**

1. **HTML** - Send immediately
2. **Critical CSS** - Inline or preload
3. **Critical JS** - Inline small scripts, preload + defer larger
4. **Fonts** - Preload critical fonts
5. **Images** - Preload hero, lazy load rest
6. **Non-critical CSS/JS** - Load async or defer

---

## Quick Wins Checklist

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- 1. Preconnect to critical origins -->
    <link rel="preconnect" href="https://fonts.googleapis.com" />

    <!-- 2. Preload critical resources -->
    <link rel="preload" href="font.woff2" as="font" crossorigin />

    <!-- 3. Inline critical CSS -->
    <style>
      /* Critical styles */
    </style>

    <!-- 4. Defer scripts -->
    <script src="app.js" defer></script>

    <!-- 5. Async third-party -->
    <script src="analytics.js" async></script>
  </head>
  <body>
    <!-- 6. Eager load hero -->
    <img src="hero.jpg" loading="eager" />

    <!-- 7. Lazy load below fold -->
    <img src="footer.jpg" loading="lazy" />

    <!-- 8. Prefetch next page -->
    <link rel="prefetch" href="/next-page" />
  </body>
</html>
```

---

## Common Mistakes

| Mistake                           | Fix                                     |
| --------------------------------- | --------------------------------------- |
| Lazy loading hero images          | Use `loading="eager"`                   |
| Blocking scripts in `<head>`      | Add `defer` or `async`                  |
| No resource hints for third-party | Add `preconnect`                        |
| Loading all images eagerly        | Use `loading="lazy"` for below-fold     |
| CSS blocks rendering              | Inline critical CSS, async non-critical |

---

## Key Takeaways

- **Preload** = critical resources you need now
- **Prefetch** = resources for next navigation
- **Lazy loading** = images/iframes below fold only
- **Defer** = app scripts that need DOM
- **Async** = independent third-party scripts
- **Critical path** = minimize render-blocking resources

**Goal:** Load what's needed, when it's needed, as fast as possible.
