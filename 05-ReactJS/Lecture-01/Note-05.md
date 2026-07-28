# React Notes — Passing Props to a Component (Revision)

## What are Props?

- **Props (Properties)** are used to pass data from a **parent** component to a **child** component.
- Similar to HTML attributes.

---

## Passing Props

```jsx
<Avatar person={person} size={100} />
```

---

## Reading Props

Using **destructuring** (recommended):

```jsx
function Avatar({ person, size }) {
  return <img />;
}
```

Equivalent to:

```jsx
function Avatar(props) {
  const person = props.person;
  const size = props.size;
}
```

---

## Props Can Be Any JavaScript Value

```jsx
name="Ayan"          // String
size={100}           // Number
isAdmin={true}       // Boolean
person={{}}          // Object
items={[]}           // Array
onClick={handleClick} // Function
```

---

## Default Props

```jsx
function Avatar({ size = 100 }) {
  // ...
}
```

- Used only when prop is **missing** or `undefined`.
- ❌ Not used for `null` or `0`.

---

## Spread Props

```jsx
<Avatar {...props} />
```

- Forwards all props.
- Use sparingly.

---

## `children` Prop

```jsx
<Card>
  <Avatar />
</Card>
```

```jsx
function Card({ children }) {
  return <div>{children}</div>;
}
```

- `children` contains everything placed between opening and closing tags.
- Commonly used for wrapper components.

---

## Props are Read-Only

❌ Don't modify props.

```jsx
props.name = "John"; // Wrong
```

Props are **immutable**.

If data needs to change, the **parent** passes new props.

---

## Props Change Over Time

Each render receives a **new snapshot** of props.

```
Parent updates
      ↓
Child receives new props
      ↓
Component re-renders
```

---

## Parent → Child Data Flow

```
Parent
   │
   │ Props
   ▼
Child
```

Data flows **one-way**: Parent → Child.

---

# Quick Recap

- Props = data passed from **parent → child**.
- Pass props like HTML attributes.
- Read props using **destructuring**.
- Props can be any JavaScript value.
- Use default values with `=`.
- `children` receives nested JSX.
- `...props` forwards all props.
- Props are **immutable (read-only)**.
- To change displayed data, the **parent passes new props** (or uses state).
