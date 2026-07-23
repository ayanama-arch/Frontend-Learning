## Big picture (anchor this first)

Embedded content answers one question:

> “Is this thing **another document**, **another runtime**, or **something I draw myself**?”

That splits cleanly into four tools.

---

## 1. `<iframe>` — embed another **HTML document**

### What it is

An `<iframe>` embeds a **separate web page** inside your page.

Different document. Different DOM. Different JS scope.

### Example

```html
<iframe src="https://example.com" width="600" height="400" title="Example site">
</iframe>
```

### Key characteristics

- Full HTML page inside a box
- Has its **own browsing context**
- Can be sandboxed for security

```html
<iframe src="page.html" sandbox></iframe>
```

### Common uses

- YouTube videos
- Maps
- Ads
- Widgets
- Payment flows

### Mental model

**Page inside a page.**

---

## 2. `<object>` and `<embed>` — embed **external non-HTML content**

These are older, heavier, and mostly legacy now.

---

### `<object>` — structured, fallback-friendly

```html
<object data="file.pdf" type="application/pdf" width="600" height="400">
  <p>PDF not supported</p>
</object>
```

**Used for**

- PDFs
- Old plugins (Flash, Java applets — dead now)

**Strength**

- Supports fallback content
- More semantic control

---

### `<embed>` — raw, minimal, no fallback

```html
<embed src="file.pdf" type="application/pdf" width="600" height="400" />
```

**Weakness**

- No fallback
- Less control
- Essentially a blunt instrument

---

### Reality check (important)

Modern web:

- `<iframe>` → YES
- `<object>` → sometimes (PDFs)
- `<embed>` → almost never

### Mental model

**Foreign object dropped into the page.**

---

## 3. SVG basics — embed **vector graphics**

### What SVG is

SVG (Scalable Vector Graphics) is **XML-based graphics**.
It’s not an image; it’s **markup**.

### Inline SVG example

```html
<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" fill="blue" />
</svg>
```

### Key properties

- Scales without blur
- CSS stylable
- JS accessible
- Part of the DOM

### Embedding SVG as a file

```html
<img src="icon.svg" alt="icon" />
```

or

```html
<object data="icon.svg" type="image/svg+xml"></object>
```

### Common uses

- Icons
- Logos
- Charts
- UI illustrations

### Mental model

**HTML for shapes.**

---

## 4. Canvas — draw with **JavaScript pixels**

### What it is

`<canvas>` gives you a **blank bitmap surface**.
You draw on it using JavaScript.

### Basic example

```html
<canvas id="box" width="200" height="100"></canvas>

<script>
  const ctx = document.getElementById("box").getContext("2d");
  ctx.fillStyle = "red";
  ctx.fillRect(20, 20, 150, 60);
</script>
```

### Key properties

- Pixel-based
- Not DOM elements
- Not accessible by default
- High performance

### Common uses

- Games
- Charts
- Animations
- Image editing
- Visualizations

### SVG vs Canvas (crucial distinction)

| SVG         | Canvas               |
| ----------- | -------------------- |
| Vector      | Bitmap               |
| DOM-based   | Pixel-based          |
| CSS + JS    | JS only              |
| Best for UI | Best for performance |

### Mental model

**A programmable drawing board.**

---

## Side-by-side clarity table

| Tool                   | What it embeds    | Control      |
| ---------------------- | ----------------- | ------------ |
| `<iframe>`             | Another HTML page | External     |
| `<object>` / `<embed>` | Non-HTML content  | External     |
| SVG                    | Vector graphics   | You          |
| Canvas                 | Pixels            | You (via JS) |

---

## One-line takeaway

- `<iframe>` embeds **documents**
- `<object>` / `<embed>` embed **foreign content**
- SVG embeds **structured graphics**
- Canvas embeds **raw drawing power**

Different eras. Different guarantees. Same goal:
**bring something into the page that HTML alone can’t express.**
