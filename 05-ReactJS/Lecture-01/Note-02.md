# React Notes — Writing Markup with JSX (Revision)

## What is JSX?

- **JSX (JavaScript XML)** is a syntax extension for JavaScript.
- Lets you write **HTML-like markup inside JavaScript**.
- React uses JSX to describe UI.

```jsx
function App() {
  return <h1>Hello</h1>;
}
```

> **JSX ≠ React**
> JSX is syntax; React is a JavaScript library.

---

# Why JSX?

- Keeps **UI (markup)** and **rendering logic (JavaScript)** together in components.
- Makes components easier to understand and maintain.

---

# Rules of JSX

## 1. Return a Single Root Element

✅ Correct

```jsx
return (
  <div>
    <h1>Hello</h1>
    <p>World</p>
  </div>
);
```

Or use a **Fragment**:

```jsx
return (
  <>
    <h1>Hello</h1>
    <p>World</p>
  </>
);
```

- `<>...</>` = **Fragment**
- Doesn't create an extra DOM element.

---

## 2. Close All Tags

HTML

```html
<img />
<li></li>
```

JSX

```jsx
<img />
<li>Hello</li>
```

Every tag must be closed.

---

## 3. Use `camelCase` for Most Attributes

HTML → JSX

| HTML           | JSX           |
| -------------- | ------------- |
| `class`        | `className`   |
| `for`          | `htmlFor`     |
| `tabindex`     | `tabIndex`    |
| `stroke-width` | `strokeWidth` |

**Exception:** `aria-*` and `data-*` remain unchanged.

```jsx
<div className="box" aria-label="Menu" data-id="123" />
```

---

# Why `className`?

- `class` is a reserved JavaScript keyword.
- React uses the DOM property name: `className`.

---

# Fragment

```jsx
<>
  <Header />
  <Main />
</>
```

- Groups multiple elements.
- Doesn't add extra HTML to the DOM.

---

# JSX vs HTML

| HTML                           | JSX                         |
| ------------------------------ | --------------------------- |
| Multiple root elements allowed | One root element required   |
| Some tags can remain unclosed  | Every tag must be closed    |
| `class`                        | `className`                 |
| Mostly lowercase attributes    | Mostly camelCase attributes |

---

# Helpful Tip

- React's error messages usually tell you exactly what's wrong with your JSX.
- HTML-to-JSX converters can automatically convert existing HTML.

---

# Quick Recap

- JSX = HTML-like syntax inside JavaScript.
- Components return **JSX**.
- Always return **one root element**.
- Close **every tag**.
- Use **camelCase** attributes (`className`, `tabIndex`, etc.).
- Use **Fragments (`<>...</>`)** to avoid unnecessary wrapper elements.
- JSX is a syntax extension; **React and JSX are separate concepts**.
