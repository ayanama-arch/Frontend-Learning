# Describing the UI

## Your First Component

## 1. What is a Component?

- A **component** is a reusable piece of UI.
- It is the **fundamental building block** of every React application.
- Technically, a React component is a **JavaScript function** that returns **JSX**.

```jsx
function Profile() {
  return <img src="image.jpg" alt="Profile" />;
}
```

---

## 2. Why Components?

Without React:

- HTML → Structure
- CSS → Styling
- JavaScript → Interactivity

With React:

- Components combine **HTML (JSX) + CSS + JavaScript** into one reusable unit.

Example:

```jsx
<TableOfContents />
<Sidebar />
<SearchBar />
```

Instead of rewriting UI repeatedly, create it once and reuse it.

---

## 3. Component Naming Rules

✅ Component names **must start with a capital letter**.

```jsx
function Profile() {}
```

❌ Wrong

```jsx
function profile() {}
```

React treats lowercase tags as HTML elements.

---

## 4. Components are JavaScript Functions

A component is simply:

```jsx
function ComponentName() {
  return JSX;
}
```

or

```jsx
const ComponentName = () => {
  return JSX;
};
```

---

## 5. Exporting Components

```jsx
export default function Profile() {
  return <img />;
}
```

`export default` makes the component available to import in other files.

```jsx
import Profile from "./Profile";
```

---

## 6. JSX

JSX is HTML-like syntax inside JavaScript.

```jsx
return <h1>Hello</h1>;
```

React converts JSX into JavaScript behind the scenes.

---

## 7. Returning JSX

### Single Line

```jsx
return <h1>Hello</h1>;
```

### Multiple Lines

Wrap JSX inside parentheses.

```jsx
return (
  <div>
    <h1>Hello</h1>
  </div>
);
```

### Why?

Without parentheses:

```jsx
return;
<div>Hello</div>;
```

JavaScript inserts a semicolon automatically.

Equivalent to

```jsx
return;

<div>Hello</div>;
```

Result:

```text
Nothing is returned.
```

---

## 8. Using Components

Components are used like HTML tags.

```jsx
function Profile() {
  return <img />;
}

export default function Gallery() {
  return (
    <>
      <Profile />
      <Profile />
      <Profile />
    </>
  );
}
```

One component can be reused many times.

---

## 9. Component Composition

Components can contain other components.

```jsx
<App>
  <Navbar />
  <Sidebar />
  <Content />
</App>
```

This is called **Component Composition**.

---

## 10. Parent & Child Components

```jsx
function Gallery() {
  return (
    <>
      <Profile />
    </>
  );
}
```

- `Gallery` → Parent
- `Profile` → Child

---

## 11. HTML Tags vs React Components

Lowercase → HTML Element

```jsx
<div>
<p>
<section>
```

Uppercase → React Component

```jsx
<Profile />
<Navbar />
<Button />
```

React distinguishes them using capitalization.

---

## 12. Browser Output

React components do **not** exist in the browser.

```jsx
<Gallery />
```

Eventually becomes

```html
<section>
  <img />
  <img />
  <img />
</section>
```

The browser only understands HTML.

---

## 13. Multiple Components in One File

Allowed:

```jsx
function Header() {}

function Footer() {}

export default function App() {}
```

Useful for:

- Small components
- Closely related components

For larger projects, place each component in its own file.

---

## 14. Never Nest Component Definitions

❌ Bad

```jsx
function App() {
  function Button() {
    return <button />;
  }
}
```

Why?

- New function created on every render
- Performance issues
- Can cause bugs (state resets)

✅ Good

```jsx
function Button() {
  return <button />;
}

function App() {
  return <Button />;
}
```

Always define components at the **top level**.

---

## 15. Passing Data

Don't nest component definitions to share data.

Instead use **props**.

```jsx
<Profile name="Ayan" />
```

---

## 16. Root Component

Every React application starts with a **root component**.

Example:

```jsx
<App />
```

or in Next.js

```jsx
pages / index.js;
```

All other components are rendered directly or indirectly from this root.

---

## 17. Components Everywhere

React apps are built entirely from components.

Examples:

- Button
- Card
- Navbar
- Sidebar
- Modal
- List
- Form
- Entire Page

Everything can be a component.

---

# Important Rules

- ✅ Components are JavaScript functions.
- ✅ Component names begin with a capital letter.
- ✅ Components return JSX.
- ✅ Use components like HTML tags (`<Profile />`).
- ✅ Components can contain other components.
- ✅ Define components at the top level.
- ✅ Reuse components instead of duplicating UI.
- ✅ Use props to pass data from parent to child.

---

## Quick Summary

| Concept          | Key Point                                                  |
| ---------------- | ---------------------------------------------------------- |
| Component        | Reusable UI building block                                 |
| React Component  | JavaScript function returning JSX                          |
| JSX              | HTML-like syntax inside JavaScript                         |
| Capital Letter   | Required for component names                               |
| `export default` | Exports the main component from a file                     |
| Parent Component | Renders child components                                   |
| Child Component  | Rendered inside a parent                                   |
| Composition      | Building UI by combining components                        |
| Root Component   | Starting point of the React app                            |
| Props            | Pass data from parent to child                             |
| Best Practice    | Define components at the top level; don't nest definitions |
