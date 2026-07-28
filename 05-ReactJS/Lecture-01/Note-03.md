# React Notes — Importing & Exporting Components (Revision)

## Why Split Components?

- Improves readability.
- Makes components reusable.
- Keeps files modular and maintainable.

---

## Root Component

- Entry point of a React app.
- Usually `App.js` (or page components in Next.js).

---

## Steps to Move a Component

1. Create a new file.
2. Export the component.
3. Import it where needed.

---

## Default Export

One per file.

**Export**

```jsx
export default function Button() {}
```

**Import**

```jsx
import Button from "./Button";
```

- Import name can be **anything**.

```jsx
import Banana from "./Button";
```

---

## Named Export

Multiple allowed per file.

**Export**

```jsx
export function Button() {}
export function Input() {}
```

**Import**

```jsx
import { Button, Input } from "./Button";
```

- Import name **must match** the exported name.

---

## Default vs Named

| Default             | Named                   |
| ------------------- | ----------------------- |
| One per file        | Multiple per file       |
| `export default`    | `export`                |
| `import X from ...` | `import { X } from ...` |
| Name can change     | Name must match         |

---

## Multiple Exports Example

```jsx
// Gallery.js
export function Profile() {}
export default function Gallery() {}
```

```jsx
// App.js
import Gallery from "./Gallery";
import { Profile } from "./Gallery";
```

---

## Best Practices

- ✅ Use **default export** when a file has one main component.
- ✅ Use **named exports** when exporting multiple components/functions.
- ✅ Give components meaningful names.
- ❌ Don't mix default and named exports unless necessary.

---

## Quick Recap

- Components can be split into separate files.
- Every React app has a root component.
- `export default` → one per file, flexible import name.
- `export` → multiple per file, import using `{}`.
- Import style must match export style.
