# Render and Commit – Revision Notes

## React UI Update Lifecycle

Every UI update happens in **3 steps**:

```text
Trigger
   ↓
Render
   ↓
Commit
   ↓
Browser Paint
```

---

# Step 1: Trigger

A render starts when:

### 1. Initial Render

```jsx
const root = createRoot(document.getElementById("root"));
root.render(<App />);
```

Called only once when the app starts.

---

### 2. State Update

```jsx
setCount(count + 1);
```

Calling a state setter **queues a re-render**.

State updates are the most common reason components render.

---

# Step 2: Render

Rendering means:

> **React calls your component functions to calculate the next UI (JSX).**

React is **not updating the DOM yet**.

Example

```jsx
function App() {
  return <Button />;
}
```

Render flow

```text
App()
   ↓
Button()
   ↓
JSX Returned
```

React recursively renders every child component.

---

# Initial Render

React calls:

```text
Root Component
      ↓
Child Components
      ↓
Grandchildren
      ↓
...
```

Until all JSX is produced.

---

# Re-render

When state changes,

React only calls the component whose state changed **and its children**.

Example

```jsx
setCount(count + 1);
```

React re-runs:

```text
Counter()
   ↓
Its Children
```

---

# Rendering is Pure

A component should behave like a **pure function**.

### Rule

Same input → Same output

```text
Props + State
      ↓
Same JSX
```

---

## Don't Cause Side Effects During Render

❌ Bad

```jsx
user.name = "John";
```

```jsx
fetch("/api");
```

```jsx
alert("Hello");
```

Rendering should only calculate JSX.

---

# Strict Mode

In development,

React may call components **twice**.

Purpose:

- Detect impure rendering.
- Find bugs early.

This happens only in development.

---

# Step 3: Commit

After rendering,

React updates the **real DOM**.

Initial render

```text
Create DOM
      ↓
appendChild()
```

Re-render

```text
Compare old UI
      ↓
Compare new UI
      ↓
Update only what's changed
```

---

# React Doesn't Recreate Everything

Example

```jsx
<>
  <h1>{time}</h1>
  <input />
</>
```

Every second:

Only

```text
<h1>
```

updates.

The

```text
<input>
```

remains untouched.

Your typed text stays.

---

# Why?

React compares

```text
Old JSX
      vs
New JSX
```

Then performs **minimal DOM updates**.

This makes React fast.

---

# Browser Paint

After React commits DOM changes,

the browser repaints the screen.

Flow

```text
Trigger
   ↓
Render
   ↓
Commit
   ↓
Browser Paint
```

---

# React Lifecycle Summary

```text
App Starts
      ↓
Initial Render
      ↓
Component Functions Execute
      ↓
JSX Produced
      ↓
DOM Updated
      ↓
Browser Paint
```

Later

```text
State Changes
      ↓
Trigger
      ↓
Render
      ↓
Commit
      ↓
Paint
```

---

# Important Points

### Trigger

- Initial render
- State update

---

### Render

- React calls components.
- Produces JSX.
- No DOM updates yet.
- Must be pure.

---

### Commit

- Updates real DOM.
- Only changes what's different.
- Doesn't recreate unchanged elements.

---

### Paint

Browser redraws the screen.

---

# Quick Revision Checklist ✅

- React updates UI in **Trigger → Render → Commit → Paint**.
- Initial render starts with `root.render(<App />)`.
- State updates (`setState`) trigger re-renders.
- Render = React calls component functions.
- Render only calculates JSX; it **doesn't touch the DOM**.
- Components should be **pure functions** (same inputs → same JSX).
- Avoid side effects during render.
- Strict Mode may render components twice in development.
- Commit phase updates the **real DOM**.
- React updates **only the changed DOM nodes**, not the whole page.
