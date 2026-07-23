# Responsive Images: The Essential Guide

## The Problem

A single `<img>` wastes bandwidth and delivers poor UX because:

- Devices have different screen sizes
- Screens have different pixel densities (1x, 2x, 3x)
- Networks have different speeds
- Some layouts need different image crops, not just different sizes

**The solution:** Give browsers multiple options and let them choose intelligently.

---

## Two Distinct Problems

### 1. Resolution Switching

Same image, different file sizes.

- **Use:** `srcset` + `sizes`
- **Example:** Product photo at 400px, 800px, 1200px widths

### 2. Art Direction

Different images with different compositions.

- **Use:** `<picture>` element
- **Example:** Landscape crop for desktop, portrait crop for mobile

**Mixing these concepts is why responsive images feel confusing.**

---

## Resolution Switching: `srcset` + `sizes`

### Basic `srcset`

```html
<img
  src="image-400.jpg"
  srcset="image-400.jpg 400w, image-800.jpg 800w, image-1200.jpg 1200w"
  alt="Product"
/>
```

- `400w` = image is 400 pixels wide
- Browser picks based on screen size, pixel density, network
- `src` is the fallback for old browsers

**Critical:** You don't control which image loads—the browser decides.

---

### Adding `sizes`

Without `sizes`, the browser assumes the image fills the entire viewport (`100vw`), which wastes bandwidth.

```html
<img
  srcset="small.jpg 400w, medium.jpg 800w, large.jpg 1200w"
  sizes="(max-width: 600px) 100vw,
         (max-width: 900px) 50vw,
         33vw"
  src="medium.jpg"
  alt="Hero image"
/>
```

**Translation:**

- Below 600px: image is 100% of viewport width
- 600–900px: image is 50% of viewport width
- Above 900px: image is 33% of viewport width

**Browser logic:**

```
Actual display width × Device Pixel Ratio = Required image width
```

Then it picks the smallest file that meets or exceeds that width.

---

## Art Direction: `<picture>`

When the **composition** needs to change, not just the size.

```html
<picture>
  <source media="(max-width: 600px)" srcset="mobile-crop.jpg" />
  <source media="(max-width: 1200px)" srcset="tablet-crop.jpg" />
  <img src="desktop-crop.jpg" alt="Hero banner" />
</picture>
```

**How it works:**

- Browser evaluates `<source>` elements top-to-bottom
- Uses the first matching media query
- Falls back to `<img>` if nothing matches

**Required:** The `<img>` tag is mandatory as a fallback.

---

## Full Power: Art Direction + Resolution Switching

Combine both techniques for maximum control:

```html
<picture>
  <!-- Mobile: tight crop + resolution options -->
  <source
    media="(max-width: 600px)"
    srcset="mobile-400.jpg 400w, mobile-800.jpg 800w"
    sizes="100vw"
  />

  <!-- Desktop: wide crop + resolution options -->
  <source
    media="(min-width: 601px)"
    srcset="
      desktop-800.jpg   800w,
      desktop-1600.jpg 1600w,
      desktop-2400.jpg 2400w
    "
    sizes="(max-width: 1200px) 80vw,
           1200px"
  />

  <img src="desktop-1600.jpg" alt="Mountain landscape" />
</picture>
```

Now you have:

- Different crops per breakpoint
- Multiple resolutions within each crop
- Optimal file selection by browser

---

## Quick Decision Tree

**Ask:** Does the image composition change between screen sizes?

**NO** → Use `<img>` with `srcset` + `sizes`

```html
<img srcset="..." sizes="..." src="..." alt="..." />
```

**YES** → Use `<picture>` with `<source>` elements

```html
<picture>
  <source media="..." srcset="..." />
  <img src="..." alt="..." />
</picture>
```

**Need both?** → Combine them (see "Full Power" example above)

---

## Common Mistakes

| Mistake                                     | Impact                                        | Fix                                   |
| ------------------------------------------- | --------------------------------------------- | ------------------------------------- |
| Using `srcset` without `sizes`              | Browser assumes `100vw`, downloads huge files | Always specify `sizes`                |
| Using `<picture>` for resolution switching  | Overcomplicated markup                        | Use `srcset` + `sizes` instead        |
| Forgetting `<img>` inside `<picture>`       | Breaks in all browsers                        | `<img>` is mandatory                  |
| Confusing `w` descriptor with media queries | Wrong image selection                         | `400w` = file width, not screen width |

---

## Real-World Example

**Scenario:** E-commerce product image

- Mobile: 1-column layout, image fills screen
- Tablet: 2-column layout, image is 50% width
- Desktop: 3-column layout, image is 33% width
- Support retina displays (2x pixel density)

```html
<img
  srcset="
    product-400.jpg   400w,
    product-800.jpg   800w,
    product-1200.jpg 1200w,
    product-1600.jpg 1600w
  "
  sizes="(max-width: 600px) 100vw,
         (max-width: 1200px) 50vw,
         33vw"
  src="product-800.jpg"
  alt="Blue ceramic vase"
/>
```

**What happens:**

- iPhone (375px wide, 2x DPR): Needs 750px → loads `product-800.jpg`
- iPad (768px wide, 50% layout, 2x DPR): Needs 768px → loads `product-800.jpg`
- Desktop (1920px wide, 33% layout, 1x DPR): Needs 640px → loads `product-800.jpg`
- Retina desktop (1920px, 33%, 2x DPR): Needs 1280px → loads `product-1600.jpg`

---

## Key Takeaway

**Responsive images = right pixels for right context**

HTML provides the options. The browser makes the optimal choice based on:

- Screen width
- Pixel density
- Network speed
- Layout constraints

Your job: Describe the options accurately. The browser handles the rest.
