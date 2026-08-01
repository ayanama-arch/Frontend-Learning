# React Notes — Keeping Components Pure (Revision)

_Based on your uploaded notes._

## What is a Pure Component?

A React component is **pure** if:

- Same **inputs (props, state, context)** → Same **JSX output**.
- Doesn't modify anything outside itself (**no side effects** during render).

---

## Pure Function Rule

```jsx id="ntx2el"
function Double({ num }) {
  return num * 2;
}
```

- `num = 3` → always `6`.
- Same input → same output.

---

## React Components Should Be Pure

```jsx id="m3dbw0"
function Recipe({ drinkers }) {
  return <p>{drinkers} cups of water</p>;
}
```

- `drinkers={2}` → always same UI.
- Output depends **only on inputs**.

---

## ❌ Impure Component

```jsx id="8qbd7e"
let guest = 0;

function Cup() {
  guest++;
  return <h2>{guest}</h2>;
}
```

Problem:

- Modifies external variable.
- Different output each render.
- Causes unpredictable bugs.

---

## ✅ Pure Version

```jsx id="7rzf1h"
function Cup({ guest }) {
  return <h2>{guest}</h2>;
}
```

Pass data through **props**, don't modify globals.

---

## Local Mutation is OK

```jsx id="je6a0g"
const items = [];

items.push("Tea");
```

✅ Allowed **if the object/array is created inside the component**.

```jsx id="l0frq0"
function App() {
  const cups = [];
  cups.push(<Cup />);
}
```

Because nothing outside the component can access it.

---

## Side Effects

Side effects include:

- API calls
- DOM manipulation
- Timers
- Animations
- Updating external variables

❌ Don't perform them during rendering.

---

## Where to Perform Side Effects?

✅ Event handlers

```jsx id="cwjlwm"
<button onClick={handleClick}>
```

✅ `useEffect()` (last resort)

```jsx id="rqarf4"
useEffect(() => {
  // Side effect
}, []);
```

---

## Never Mutate

Don't directly modify:

- Props
- State
- Context
- External variables

Instead, **update state** using React's state setters.

---

## Strict Mode

- Helps detect impure components.
- May render components twice in development.
- Helps find side effects and mutations.

---

# Quick Recap

- Components should be **pure**.
- Same inputs → same JSX.
- Don't modify variables outside the component.
- **Local mutation** is okay.
- Perform side effects in **event handlers** or **`useEffect()`**.
- Never mutate **props, state, or context** directly.
- **Strict Mode** helps catch impure rendering bugs.
