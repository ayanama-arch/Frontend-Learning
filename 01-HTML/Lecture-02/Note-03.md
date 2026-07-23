## Big picture first (mental model)

HTML media works like this:

- `<audio>` / `<video>` → **the player**
- `<source>` → **where the media comes from**
- `<track>` → **extra data layered on top (captions, subtitles, metadata)**

Think: **container → sources → annotations**.

---

## 1. Audio element (`<audio>`)

### What it is

Embeds **sound** into the page with native playback controls.

### Basic example

```html
<audio controls>
  <source src="music.mp3" type="audio/mpeg" />
  Your browser does not support audio.
</audio>
```

### Key attributes

- `controls` → play/pause UI
- `autoplay` → starts automatically (often blocked)
- `loop` → repeats
- `muted` → starts silent
- `preload` → metadata | auto | none

### When to use

- Music
- Podcasts
- Voice notes
- Sound effects

---

## 2. Video element (`<video>`)

### What it is

Embeds **video + audio + visuals**.

### Basic example

```html
<video controls width="400">
  <source src="movie.mp4" type="video/mp4" />
  Your browser does not support video.
</video>
```

### Key attributes

- `controls`
- `width` / `height`
- `poster` → thumbnail image
- `autoplay` (usually requires `muted`)
- `loop`

### When to use

- Tutorials
- Demos
- Product videos
- Media playback without external players

---

## 3. Source element (`<source>`)

### What it is

Defines **multiple media formats** so the browser can choose the one it supports.

### Why it exists

Different browsers support different codecs.

### Example with fallback

```html
<video controls>
  <source src="video.webm" type="video/webm" />
  <source src="video.mp4" type="video/mp4" />
  Your browser does not support video.
</video>
```

### How the browser behaves

- Tries sources **top to bottom**
- Plays the **first supported format**

### Important rule

`<source>` is **meaningless alone**.
It must live inside `<audio>` or `<video>`.

---

## 4. Track element (`<track>`)

### What it is

Adds **time-based text** to media:

- Captions
- Subtitles
- Descriptions
- Chapters

### Accessibility-critical element

### Example with captions

```html
<video controls>
  <source src="lecture.mp4" type="video/mp4" />
  <track
    src="captions.vtt"
    kind="subtitles"
    srclang="en"
    label="English"
    default
  />
</video>
```

### Key attributes

- `kind` → subtitles | captions | descriptions | chapters | metadata
- `srclang` → language code
- `label` → user-facing name
- `default` → enabled by default

### File format

Uses **WebVTT (`.vtt`)**:

```text
00:00:01.000 --> 00:00:04.000
Welcome to the course.
```

---

## How all four work together (full example)

```html
<video controls poster="thumb.jpg">
  <source src="video.webm" type="video/webm" />
  <source src="video.mp4" type="video/mp4" />

  <track
    src="sub-en.vtt"
    kind="subtitles"
    srclang="en"
    label="English"
    default
  />
  <track src="sub-hi.vtt" kind="subtitles" srclang="hi" label="Hindi" />

  Your browser does not support video.
</video>
```

This gives:

- Player UI
- Multiple formats
- Multiple languages
- Accessibility support
- Graceful fallback

---

## Decision table (quick recall)

| Element    | Role                            |
| ---------- | ------------------------------- |
| `<audio>`  | Sound player                    |
| `<video>`  | Visual + sound player           |
| `<source>` | Media file options              |
| `<track>`  | Captions / subtitles / metadata |

---

## One-line takeaway

`<audio>` and `<video>` **play media**,
`<source>` **feeds them options**,
`<track>` **makes them understandable to humans and machines**.
