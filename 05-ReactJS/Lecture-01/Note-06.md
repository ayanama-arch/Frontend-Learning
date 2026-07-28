# React Notes — Conditional Rendering (Revision)

## What is Conditional Rendering?

- Render different JSX based on a condition.
- Uses normal **JavaScript** (`if`, `?:`, `&&`).

---

## 1. `if` Statement

Best for complex conditions.

```jsx
if (isPacked) {
  return <li>{name} ✅</li>;
}
return <li>{name}</li>;
```

---

## 2. Return `null`

Render nothing.

```jsx
if (isPacked) {
  return null;
}
```

> `null` = render nothing.

---

## 3. Ternary Operator (`? :`)

Choose between two values.

```jsx
<li>{isPacked ? name + " ✅" : name}</li>
```

Syntax:

```jsx
condition ? valueIfTrue : valueIfFalse;
```

---

## 4. Logical AND (`&&`)

Render only when condition is true.

```jsx
<li>
  {name} {isPacked && "✅"}
</li>
```

Equivalent to:

```jsx
if (isPacked) {
  render "✅";
}
```

---

## 5. Store JSX in a Variable

Useful for complex logic.

```jsx
let content = name;

if (isPacked) {
  content = <del>{name} ✅</del>;
}

return <li>{content}</li>;
```

---

## 6. `&&` Pitfall

❌ Wrong

```jsx
{
  count && <p>Messages</p>;
}
```

If `count = 0`, React renders:

```text
0
```

✅ Correct

```jsx
{
  count > 0 && <p>Messages</p>;
}
```

---

## Which One to Use?

| Syntax        | Use When                           |
| ------------- | ---------------------------------- |
| `if`          | Complex conditions                 |
| `return null` | Render nothing                     |
| `?:`          | Two alternatives                   |
| `&&`          | Render only if true                |
| Variable      | Complex JSX or multiple conditions |

---

# Quick Recap

- React uses **JavaScript** for conditional rendering.
- `if` → different JSX.
- `null` → render nothing.
- `?:` → choose between two outputs.
- `&&` → render only when condition is true.
- Store JSX in variables for cleaner code.
- Avoid using numbers on the left side of `&&` (e.g., `0 && ...`).
