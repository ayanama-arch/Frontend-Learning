# React Notes — Rendering Lists (Revision)

## Why Render Lists?

- Display multiple similar components from an array.
- Mainly use **`map()`** and **`filter()`**.

---

## 1. `map()` – Render Lists

Converts an array into JSX.

```jsx id="6smq9g"
const listItems = people.map((person) => (
  <li key={person.id}>{person.name}</li>
));
```

```jsx id="szm6wd"
return <ul>{listItems}</ul>;
```

---

## 2. `filter()` – Filter Data

Returns only matching items.

```jsx id="vubkl4"
const chemists = people.filter((person) => person.profession === "chemist");
```

Often used before `map()`.

```jsx id="v2gob2"
people
  .filter(...)
  .map(...)
```

---

## 3. `map()` + `filter()`

```jsx id="kkc1y7"
people
  .filter((person) => person.profession === "chemist")
  .map((person) => <li key={person.id}>{person.name}</li>);
```

---

## 4. Arrow Function Return

**Implicit Return**

```jsx id="cnl26n"
people.map((person) => <li>{person.name}</li>);
```

**Block Body (Needs `return`)**

```jsx id="3j90oz"
people.map((person) => {
  return <li>{person.name}</li>;
});
```

---

## 5. `key` Prop

Every element inside `map()` **must** have a unique `key`.

```jsx id="0mj8aj"
<li key={person.id}>
```

Purpose:

- Helps React identify items.
- Improves updates and performance.
- Prevents rendering bugs.

---

## Good Keys

- Database IDs
- UUIDs
- Stable unique IDs

```jsx id="0vrgwj"
key={person.id}
```

---

## Avoid These Keys

❌ Array index

```jsx id="n5y2dn"
key = { index };
```

❌ Random values

```jsx id="qm8uor"
key={Math.random()}
```

Keys should be **stable** between renders.

---

## Key Rules

- ✅ Unique among siblings.
- ✅ Stable (don't change).
- ❌ Not passed as a prop.

```jsx id="92glty"
<Profile key={id} userId={id} />
```

Inside `Profile`, you can access `userId`, **not** `key`.

---

## Quick Recap

- Store data in **arrays/objects**, not hardcoded JSX.
- Use **`map()`** to render lists.
- Use **`filter()`** to select specific items.
- Every item in `map()` needs a **unique `key`**.
- Prefer **stable IDs**, avoid `index` and `Math.random()`.
- Arrow functions with `{}` require an explicit `return`.
