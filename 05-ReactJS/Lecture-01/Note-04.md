# React Notes — JavaScript in JSX with Curly Braces (Revision)

## Curly Braces `{}` in JSX

- `{}` lets you write **JavaScript expressions inside JSX**.
- Think of it as a **window from JSX into JavaScript**.

---

## 1. Strings

**Static String**

```jsx
<img src="image.jpg" alt="Avatar" />
```

**Dynamic String (Variable)**

```jsx
const avatar = "image.jpg";

<img src={avatar} />;
```

---

## 2. Display Variables

```jsx
const name = "Gregorio";

<h1>{name}</h1>;
```

---

## 3. Use JavaScript Expressions

```jsx
const age = 22;

<p>{age + 1}</p>;
```

```jsx
<p>{2 * 10}</p>
```

Any valid JavaScript expression works.

---

## 4. Call Functions

```jsx
function greet() {
  return "Hello";
}

<h1>{greet()}</h1>;
```

---

## 5. Use Objects

```jsx
const person = {
  name: "Gregorio",
};

<h1>{person.name}</h1>;
```

---

## 6. Inline Styles (`{{ }}`)

```jsx
<div
  style={{
    backgroundColor: "black",
    color: "pink"
  }}
>
```

- Outer `{}` → JavaScript expression.
- Inner `{}` → JavaScript object.

`{{ }}` = **Object inside JSX expression**.

---

## 7. Style Properties

Use **camelCase**.

| CSS                | JSX               |
| ------------------ | ----------------- |
| `background-color` | `backgroundColor` |
| `font-size`        | `fontSize`        |
| `text-align`       | `textAlign`       |

---

## 8. Where Can `{}` Be Used?

### Inside JSX content

```jsx
<h1>{name}</h1>
```

### In JSX attributes

```jsx
<img src={avatar} />
```

❌ Wrong

```jsx
src = "{avatar}";
```

This passes the literal string `"{avatar}"`.

---

## 9. Quotes vs Curly Braces

```jsx
title="Hello"     // String

title={name}      // Variable

title={2 + 2}     // Expression

title={getTitle()} // Function call
```

---

# Quick Recap

- `{}` = JavaScript inside JSX.
- Use quotes (`""`) for static strings.
- Use `{}` for variables, expressions, functions, and objects.
- `{{ }}` = JavaScript object (commonly for `style`).
- Inline styles use **camelCase**.
- Curly braces work:
  - Inside JSX content.
  - After `=` in JSX attributes.
