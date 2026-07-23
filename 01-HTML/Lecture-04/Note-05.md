# Cutting-edge HTML APIs

```
Modern HTML

├── View Transitions API
├── Speculation Rules API
├── Core Web Vitals Optimization
└── HTML Fragments
```

---

# Why were these APIs introduced?

The web has evolved through three major eras.

## Era 1 — Static Documents

HTML pages looked like books.

```
Browser

↓

Load HTML

↓

Display

↓

Done
```

Every click loaded an entirely new page.

---

## Era 2 — Dynamic Websites

JavaScript started modifying pages.

```
User Click

↓

AJAX

↓

Update Some Elements

↓

No Page Reload
```

Better, but still limited.

---

## Era 3 — Application-like Websites

Today users expect

- instant navigation
- smooth animations
- zero waiting
- native app experience

Modern HTML APIs exist to make browsers do these efficiently.

---

# 1. View Transitions API

## The Problem

Traditional navigation

```
Page A

↓

Click Link

↓

White Screen

↓

Page B
```

Looks abrupt.

---

Single Page Applications (React, Vue, Next.js) improved this.

```
Fade Out

↓

Animate

↓

Fade In
```

But developers had to write lots of JavaScript.

Browsers now provide this natively.

---

# What is View Transition?

It lets the browser animate between two visual states.

Instead of

```
Old Page

↓

Instant Replacement

↓

New Page
```

It becomes

```
Old Page

↓

Capture Snapshot

↓

Animate

↓

New Page
```

The browser creates screenshots of both states and animates them.

---

## Basic Example

```javascript
document.startViewTransition(() => {
  document.body.classList.toggle("dark");
});
```

Instead of instantly changing

```
Light Theme

↓

Dark Theme
```

the browser smoothly morphs between them.

---

## HTML

```html
<button id="theme">Change Theme</button>
```

```javascript
theme.onclick = () => {
  document.startViewTransition(() => {
    document.body.classList.toggle("dark");
  });
};
```

---

## Cross-page Transitions

Suppose

```
Home

↓

Products

↓

Cart
```

Normally

```
Load

↓

Blank

↓

New Page
```

With View Transition

```
Fade

↓

Slide

↓

Morph

↓

Done
```

No JavaScript animation library required.

---

## Shared Elements

Suppose a product image exists on both pages.

Old

```
📱
```

New

```
            📱
```

Instead of disappearing,

it moves.

```
📱

↓

Animation

↓

             📱
```

The browser understands they're the same element.

```css
.product-image {
  view-transition-name: phone;
}
```

---

# Advantages

- GPU accelerated
- Native
- Smooth
- Less JavaScript
- Better performance

---

# Limitations

- Browser support still evolving.
- Complex transitions may still need custom animation.

---

# 2. Speculation Rules API

One of the coolest browser APIs.

---

## The Problem

Suppose you're reading

```
Home

Products

About

Contact
```

You click

```
Products
```

The browser starts

```
DNS

↓

TCP

↓

TLS

↓

Request

↓

HTML

↓

CSS

↓

JS

↓

Render
```

This can take hundreds of milliseconds.

---

But what if the browser already knew what you'd likely click?

Then it could prepare ahead of time.

---

# Idea

Predict the future.

```
User probably clicks here

↓

Load beforehand

↓

Instant navigation
```

---

# Speculation Rules

Instead of JavaScript,

you declare rules.

```html
<script type="speculationrules">
  {
    "prefetch": [
      {
        "source": "document"
      }
    ]
  }
</script>
```

The browser decides

```
Likely Page

↓

Prefetch

↓

Store

↓

Instant Load
```

---

## Prefetch

Downloads resources early.

```
Click

↓

Already Downloaded

↓

Fast
```

---

## Prerender

Even more powerful.

Browser loads the next page in the background.

```
Current Page

↓

Hidden Tab

↓

Render

↓

User Clicks

↓

Instant
```

Feels like magic.

---

## Example

```json
{
  "prerender": [
    {
      "urls": ["/products", "/pricing"]
    }
  ]
}
```

The browser prepares those pages before you visit them.

---

## Why is it better than JavaScript?

Old way

```
Mouse Hover

↓

JavaScript

↓

Fetch
```

New

```
Browser decides intelligently.
```

Lower CPU usage.

Smarter scheduling.

---

# Benefits

- Faster navigation
- Lower latency
- Better UX
- Better Core Web Vitals

---

# Drawbacks

May download pages users never visit.

Browsers carefully limit unnecessary work.

---

# 3. Core Web Vitals Optimization

This is not a single API.

It is a collection of metrics Google uses to measure user experience.

Think of it as

```
Website Quality Score
```

---

# Why?

Old metrics

```
Load Time
```

weren't enough.

Suppose

```
Page loaded

↓

Button still unusable

↓

Images jump

↓

Text moves

↓

Lag
```

Technically loaded.

Practically terrible.

---

Google introduced Core Web Vitals.

---

# Three Major Metrics

```
Core Web Vitals

├── LCP
├── INP
└── CLS
```

---

# LCP

Largest Contentful Paint

Measures

> How quickly the main content becomes visible.

Usually

```
Hero Image

or

Main Heading
```

Ideal

```
Under 2.5 seconds
```

---

Example

```
Loading...

↓

Hero Image

↓

Done
```

LCP measures when the hero appears.

---

# INP

Interaction to Next Paint

Measures

```
User Click

↓

Browser Responds
```

Bad

```
Click

...

...

300ms

↓

Response
```

Good

```
Click

↓

Immediate Feedback
```

Target

```
Less than 200ms
```

INP replaced the older First Input Delay (FID) metric.

---

# CLS

Cumulative Layout Shift

Measures unexpected movement.

Bad

```
Click Login

↓

Advertisement loads

↓

Button moves

↓

Wrong Click
```

Layout shifts increase CLS.

---

Example

Bad

```
Hello



(Image Loads)

↓

Everything Moves
```

Good

Reserve image space.

```html
<img width="600" height="400" src="hero.jpg" alt="" />
```

Nothing shifts.

---

# Optimizing Core Web Vitals

## Improve LCP

- Optimize images
- Compress assets
- Reduce server response time
- Use modern image formats (WebP, AVIF)
- Lazy-load non-critical images
- Preload critical resources

```html
<link rel="preload" href="/hero.webp" as="image" />
```

---

## Improve INP

- Reduce long JavaScript tasks
- Split large bundles
- Use event delegation where appropriate
- Avoid blocking the main thread

---

## Improve CLS

Always specify image dimensions.

```html
<img src="banner.jpg" width="800" height="400" />
```

Reserve space for ads and embeds.

Avoid inserting content above existing content after the page has rendered.

---

# Why HTML Matters Here

Good HTML directly improves these metrics.

Examples

```
loading="lazy"

decoding="async"

fetchpriority="high"

preload

picture

srcset
```

Modern HTML helps browsers make better loading decisions.

---

# 4. HTML Fragments

This topic can mean different things depending on the context. In modern web development, it most commonly refers to **partial HTML documents** that are fetched and inserted into an existing page instead of reloading the entire document.

---

## Traditional Navigation

```
Browser

↓

Request

↓

Entire HTML

↓

Render
```

Every navigation transfers a full HTML document.

---

## Fragment-based Navigation

```
Browser

↓

Request

↓

Only Needed HTML

↓

Insert Into DOM
```

Example response:

```html
<article>
  <h2>Latest News</h2>
  <p>Content...</p>
</article>
```

Instead of replacing the whole page, JavaScript inserts only this fragment.

```javascript
const html = await fetch("/news/fragment").then((r) => r.text());

document.querySelector("#content").innerHTML = html;
```

This approach reduces transferred data and can make updates feel instant.

> **Note:** There is no standardized `<fragment>` HTML element. "HTML fragments" describe a pattern used by frameworks and servers. Libraries and frameworks such as HTMX, Turbo, and modern server-rendered frameworks commonly exchange HTML fragments rather than JSON for UI updates.

---

# Comparison

| Feature           | Purpose                                | Benefit                               |
| ----------------- | -------------------------------------- | ------------------------------------- |
| View Transitions  | Smoothly animate between UI states     | Native page/app-like transitions      |
| Speculation Rules | Predict and preload likely navigations | Faster navigation                     |
| Core Web Vitals   | Measure and optimize user experience   | Better performance and SEO visibility |
| HTML Fragments    | Send only the required HTML            | Less data transfer and faster updates |

---

# How They Work Together

Imagine an e-commerce site.

```
User Opens Home

↓

Speculation Rules prefetch Products

↓

User Clicks Products

↓

View Transition animates navigation

↓

Only Product Grid HTML Fragment loads

↓

Images use lazy loading, dimensions, and preload

↓

Excellent Core Web Vitals
```

The result feels much closer to a native mobile app than a traditional website.

---

# Interview Questions

1. What problem does the View Transitions API solve?
2. How does `document.startViewTransition()` work?
3. What is the difference between **prefetch** and **prerender** in the Speculation Rules API?
4. What are the three Core Web Vitals, and what does each measure?
5. How can HTML improve LCP, INP, and CLS?
6. What are HTML fragments, and how are they different from full HTML documents?
7. Why are HTML fragments commonly used in modern server-rendered applications?
8. When would you choose HTML fragments over returning JSON from an API?

## Key Takeaway

These APIs shift responsibility from JavaScript libraries to the browser itself. Instead of manually orchestrating navigation, prediction, rendering, and performance, you **declare intent**, and the browser uses its internal knowledge of networking, rendering, and scheduling to produce a faster, smoother, and more efficient user experience.
