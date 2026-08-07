# React State as a Snapshot – Revision Notes

# Core Idea

**State is a snapshot, not a mutable variable.**

Calling `setState()` **does not change the current state**.
It schedules a **new render** with the updated state.

---

# How State Updates Work

```text
User Action
      ↓
setState()
      ↓
React Schedules Re-render
      ↓
Component Executes Again
      ↓
New State Snapshot
```

State changes are visible **only in the next render**.

---

# State Lives Outside the Component

State is **stored by React**, not inside your function.

```text
React
 ├── count = 0
 ├── user = "Alice"
 └── theme = "Dark"
```

Each render receives a **snapshot** of those values.

---

# Every Render Gets Its Own Snapshot

```jsx
const [count, setCount] = useState(0);
```

Render 1

```text
count = 0
```

After

```jsx
setCount(1);
```

Render 2

```text
count = 1
```

The old render **never changes**.

---

# `setState()` Doesn't Update Immediately

```jsx
setCount(count + 1);

console.log(count);
```

Output

```text
Old Value
```

Because `count` belongs to the current render.

---

# Why `+3` Only Adds 1

```jsx
setCount(count + 1);
setCount(count + 1);
setCount(count + 1);
```

Current render:

```text
count = 0
```

React receives

```text
setCount(1)
setCount(1)
setCount(1)
```

Final state

```text
count = 1
```

Not `3`.

---

# Think of State as Value Substitution

Instead of

```jsx
setCount(count + 1);
```

Imagine

```jsx
setCount(0 + 1);
```

Every call becomes

```jsx
setCount(1);
setCount(1);
setCount(1);
```

Makes React's behavior easier to understand.

---

# Event Handlers Use the Snapshot

```jsx
<button onClick={() => {
    setCount(count + 5);
    alert(count);
}}>
```

If

```text
count = 0
```

Then

```text
Alert → 0
```

Not `5`.

---

# Even Async Functions Keep the Same Snapshot

```jsx
setCount(count + 5);

setTimeout(() => {
  alert(count);
}, 3000);
```

Still shows

```text
0
```

Even after 3 seconds.

Reason:

The callback remembers the **state snapshot** from when it was created.

---

# Event Handlers Never See Future State

Every event handler belongs to a specific render.

```text
Render 1
    ↓
Creates onClick()
    ↓
Uses count = 0 forever
```

Later renders create **new event handlers** with updated state.

---

# Snapshot Example

Render 1

```text
count = 0
```

Button

```jsx
() => {
  setCount(1);
  alert(count);
};
```

Actually behaves like

```jsx
() => {
  setCount(1);
  alert(0);
};
```

---

# Re-render Creates New Handlers

Render 2

```text
count = 1
```

New handler

```jsx
() => {
  setCount(2);
  alert(1);
};
```

Each render gets a **fresh copy** of event handlers.

---

# Why React Uses Snapshots

Benefits:

- Predictable behavior.
- No accidental changes during execution.
- Async code behaves consistently.
- Fewer timing bugs.

---

# Important Mental Model

Component executes

```text
Props + State Snapshot
        ↓
JSX
        ↓
Event Handlers
```

Everything created during that render uses the **same snapshot**.

---

# State vs Snapshot

| State                   | Snapshot                         |
| ----------------------- | -------------------------------- |
| Stored by React         | Value received during one render |
| Can change              | Never changes during that render |
| Used for future renders | Used by current render           |

---

# Quick Revision Checklist ✅

- State behaves like a **snapshot**, not a normal variable.
- `setState()` schedules the **next render**.
- Current state never changes during the current render.
- React stores state outside the component.
- Every render gets its own **state snapshot**.
- Event handlers capture the snapshot from the render that created them.
- `setState()` does **not** immediately update the variable.
- Multiple `setState(count + 1)` calls in one render use the **same old value**.
- Async callbacks (`setTimeout`, promises, etc.) also use the snapshot from their render.
- Every re-render creates **new event handlers** with a fresh state snapshot.
