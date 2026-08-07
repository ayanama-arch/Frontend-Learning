# 1. CSS Basics ✅

## What is CSS?

CSS (**Cascading Style Sheets**) is used to style HTML elements (colors, fonts, spacing, layouts).

```html
<p>Hello World</p>
```

```css
p {
  color: blue;
}
```

---

## CSS Syntax

```css
selector {
  property: value;
}
```

Example:

```css
h1 {
  color: red;
  font-size: 32px;
}
```

- **Selector** → selects element
- **Property** → what to change
- **Value** → new setting

---

## Ways to Add CSS

### Inline

```html
<h1 style="color:red;">Hello</h1>
```

---

### Internal

```html
<style>
  h1 {
    color: red;
  }
</style>
```

---

### External (Recommended)

```html
<link rel="stylesheet" href="style.css" />
```

```css
h1 {
  color: red;
}
```

---

## Comments

```css
/* This is a comment */
```

---

# 2. Selectors Fundamentals ✅

## Element Selector

Targets all elements.

```css
p {
  color: blue;
}
```

---

## Class Selector

Starts with `.`

```html
<p class="info">Hello</p>
```

```css
.info {
  color: green;
}
```

---

## ID Selector

Starts with `#`

```html
<h1 id="title">Welcome</h1>
```

```css
#title {
  color: red;
}
```

> IDs should be unique.

---

## Universal Selector

Targets every element.

```css
* {
  margin: 0;
  padding: 0;
}
```

---

## Grouping Selector

Apply same style to multiple selectors.

```css
h1,
h2,
p {
  color: blue;
}
```

---

# 3. Text and Font Properties ✅

## Font Family

```css
p {
  font-family: Arial, sans-serif;
}
```

---

## Font Size

```css
p {
  font-size: 20px;
}
```

---

## Font Weight

```css
p {
  font-weight: bold;
}
```

or

```css
font-weight: 700;
```

---

## Text Color

```css
color: blue;
```

---

## Text Alignment

```css
text-align: center;
```

Values:

- left
- center
- right
- justify

---

## Text Decoration

```css
text-decoration: underline;
```

Remove links underline:

```css
a {
  text-decoration: none;
}
```

---

## Line Height

Space between lines.

```css
line-height: 1.6;
```

---

## Letter Spacing

```css
letter-spacing: 2px;
```

---

## Text Transform

```css
text-transform: uppercase;
```

Values:

- uppercase
- lowercase
- capitalize

---

# 4. Colors and Backgrounds ✅

## Color Values

### Named

```css
color: red;
```

### Hex

```css
color: #3498db;
```

### RGB

```css
color: rgb(52, 152, 219);
```

---

## Background Color

```css
background-color: yellow;
```

---

## Background Image

```css
background-image: url("bg.jpg");
```

---

## Background Repeat

```css
background-repeat: no-repeat;
```

---

## Background Position

```css
background-position: center;
```

---

## Background Size

```css
background-size: cover;
```

---

## Opacity

```css
opacity: 0.5;
```

Range:

```
0 → invisible
1 → fully visible
```

---

## Transparency (RGBA)

```css
background: rgba(255, 0, 0, 0.5);
```

---

# 5. Box Model Fundamentals ✅

Every element consists of:

```
Margin
 Border
  Padding
   Content
```

---

## Width & Height

```css
width: 300px;
height: 200px;
```

---

## Padding

Space inside border.

```css
padding: 20px;
```

---

## Margin

Space outside border.

```css
margin: 20px;
```

---

## Border

```css
border: 2px solid black;
```

---

## Box Sizing

```css
box-sizing: border-box;
```

Includes padding and border inside the width.

---

## Border Styles

```css
border-style: solid;
border-width: 2px;
border-color: red;
```

Common styles:

- solid
- dashed
- dotted
- double

---

# 6. Basic Layout ✅

## Display Property

### Block

Starts on new line.

```css
display: block;
```

Examples:

- div
- p
- h1

---

### Inline

Only takes required width.

```css
display: inline;
```

Examples:

- span
- a

---

### Inline-block

Inline but width & height work.

```css
display: inline-block;
```

---

## Float

Moves element left/right.

```css
float: left;
```

---

## Clear

Stops floating.

```css
clear: both;
```

---

## Position: Static

Default positioning.

```css
position: static;
```

---

## Position: Relative

Moves relative to original position.

```css
position: relative;
left: 20px;
top: 10px;
```

---

## Basic Centering

### Horizontal

```css
width: 300px;
margin: auto;
```

---

### Flexbox (modern)

```css
display: flex;
justify-content: center;
align-items: center;
```

---

# 7. Lists and Links ✅

## List Style

```css
list-style: square;
```

or

```css
list-style: none;
```

---

## Link States

```css
a:link {
  color: blue;
}

a:visited {
  color: purple;
}

a:hover {
  color: red;
}

a:active {
  color: green;
}
```

Remember order:

```
LVHA

Link
Visited
Hover
Active
```

---

## Remove Default Styles

```css
ul {
  list-style: none;
}

a {
  text-decoration: none;
}
```

---

## Simple Navigation

```html
<ul>
  <li><a href="#">Home</a></li>
  <li><a href="#">About</a></li>
</ul>
```

```css
li {
  display: inline-block;
  margin-right: 20px;
}
```

---

# 8. Units and Measurements ✅

## Absolute Units

| Unit | Meaning              |
| ---- | -------------------- |
| px   | Pixels (most common) |
| pt   | Points (print)       |
| cm   | Centimeters (print)  |

Example:

```css
font-size: 18px;
```

---

## Relative Units

### em

Relative to parent font size.

```css
font-size: 2em;
```

---

### rem

Relative to root (`html`) font size.

```css
font-size: 2rem;
```

---

### %

Relative to parent size.

```css
width: 50%;
```

---

## Viewport Units

```css
width: 100vw;
height: 100vh;
```

- **vw** = viewport width
- **vh** = viewport height

---

## When to Use Each Unit

| Unit  | Use Case                          |
| ----- | --------------------------------- |
| px    | Borders, icons, fixed sizes       |
| rem   | Font sizes, spacing (recommended) |
| em    | Component-relative sizing         |
| %     | Responsive widths                 |
| vh/vw | Full-screen sections              |
| pt/cm | Printing only                     |

---

# 📌 Quick Revision

| Topic         | Most Used Properties                                      |
| ------------- | --------------------------------------------------------- |
| CSS Basics    | `color`, `font-size`                                      |
| Selectors     | `.class`, `#id`, `*`                                      |
| Text          | `font-family`, `text-align`, `line-height`                |
| Background    | `background-color`, `background-image`, `background-size` |
| Box Model     | `margin`, `padding`, `border`, `box-sizing`               |
| Layout        | `display`, `position`, `float`, `margin:auto`             |
| Lists & Links | `list-style`, `text-decoration`, `:hover`                 |
| Units         | `px`, `rem`, `%`, `vw`, `vh`                              |
