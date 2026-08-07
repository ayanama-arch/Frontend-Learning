# React State (`useState`) – Revision Notes

# What is State?

State is a component's **memory**.

It stores data that:

- Changes over time.
- Must persist between renders.
- Causes the UI to update.

Examples:

- Counter value
- Input field
- Current image
- Shopping cart
- Dark mode

---

# Why Normal Variables Don't Work

```jsx
let count = 0;
```

Problems:

❌ Doesn't persist after re-render.

❌ Updating it doesn't trigger a re-render.

React recreates local variables every render.

---

# Solution: `useState`

```jsx
import { useState } from "react";
```

```jsx
const [count, setCount] = useState(0);
```

React now:

- Remembers the value.
- Re-renders when it changes.

---

# Syntax

```jsx
const [state, setState] = useState(initialValue);
```

Example

```jsx
const [count, setCount] = useState(0);
```

- `count` → current state
- `setCount()` → updates state
- `0` → initial value

---

# Updating State

```jsx
setCount(count + 1);
```

Never do:

```jsx
count = count + 1;
```

Only use the setter.

---

# What `useState()` Returns

It returns an array:

```jsx
const [state, setState] = useState(initialValue);
```

Equivalent to:

```jsx
const arr = useState(0);

const state = arr[0];
const setState = arr[1];
```

Uses **array destructuring**.

---

# How State Works

First render

```jsx
const [count, setCount] = useState(0);
```

React stores

```text
count = 0
```

Click button

```jsx
setCount(1);
```

React

1. Updates state.
2. Re-renders component.
3. Returns new value.

Now

```text
count = 1
```

---

# Hooks

A Hook is any function starting with:

```text
use...
```

Examples

- useState
- useEffect
- useRef
- useMemo

Hooks let you use React features.

---

# Rules of Hooks

✅ Call Hooks only at the top level.

```jsx
const [count, setCount] = useState(0);
```

❌ Don't call inside

```jsx
if (...) {}
for (...) {}
while (...) {}
function() {}
```

Hooks must always execute in the same order.

---

# Naming Convention

```jsx
const [name, setName] = useState("");
```

Pattern

```text
[state, setState]
```

Examples

```jsx
const [count, setCount];
const [user, setUser];
const [theme, setTheme];
const [loading, setLoading];
```

---

# Multiple State Variables

You can have many states.

```jsx
const [count, setCount] = useState(0);
const [showMore, setShowMore] = useState(false);
const [name, setName] = useState("");
```

Use separate state when values are unrelated.

---

# Combine State When Related

Instead of

```jsx
const [firstName, setFirstName];
const [lastName, setLastName];
```

Sometimes better

```jsx
const [user, setUser] = useState({
  firstName: "",
  lastName: "",
});
```

Use one object if values usually change together.

---

# State is Local

Every component instance gets its own state.

```jsx
<Counter />
<Counter />
```

Each counter has independent values.

Changing one won't affect the other.

---

# State is Private

Only the component that owns the state can access or update it.

Parent **cannot directly modify** child's state.

To share state:

- Lift state to the closest common parent.

---

# State vs Normal Variable

| Normal Variable       | State                    |
| --------------------- | ------------------------ |
| Lost after render     | Persists between renders |
| Doesn't update UI     | Triggers re-render       |
| React ignores changes | React tracks changes     |

---

# Re-render Flow

```text
Initial Render
      ↓
User Action
      ↓
setState()
      ↓
State Updated
      ↓
React Re-renders
      ↓
Updated UI
```

---

# Quick Revision Checklist ✅

- State = component memory.
- Use state for values that change over time.
- Normal variables don't persist across renders.
- `useState(initialValue)` creates state.
- `useState` returns `[state, setter]`.
- Always update state using the setter.
- `setState()` triggers a re-render.
- Hooks always start with `use`.
- Hooks must be called only at the top level.
- One component can have multiple state variables.
- Combine related state into one object.
- State is local and private to each component instance.
