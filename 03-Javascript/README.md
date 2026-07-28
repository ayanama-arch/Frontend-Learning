# JavaScript in HTML

## `<script>` Tag

- Used to add JavaScript to HTML.
- Browser executes it immediately when encountered.

```html
<script>
  console.log("Hello");
</script>
```

---

## Inline vs External Script

**Inline**

```html
<script>
  alert("Hi");
</script>
```

**External**

```html
<script src="app.js"></script>
```

> ✅ Use external files for larger projects.

---

## `src` Attribute

Loads an external JavaScript file.

```html
<script src="app.js"></script>
```

Supports:

- Relative path → `script.js`
- Absolute path → `/js/script.js`
- Full URL → `https://...`

---

## Execution Order

Browser parses HTML **top → bottom**.

```
HTML
↓
<script>
↓
Execute JS
↓
Continue HTML
```

Scripts execute in the order they appear.

---

## Browser Cache

- External JS is downloaded once.
- Stored in cache.
- Reused on future visits.
- Improves performance.

---

## Important Rule

❌ Invalid

```html
<script src="app.js">
  alert("Hello");
</script>
```

When `src` exists, **inline code is ignored**.

---

## Deprecated Attributes

```html
type="text/javascript" language="JavaScript"
```

❌ No longer needed in HTML5.

---

## Why External JS?

- Cleaner HTML
- Reusable
- Easier maintenance
- Browser caching
- Faster loading

---

## Browser vs Node.js

**Browser**

- Runs inside web pages.
- Has `window`, `document`, `alert()`.

**Node.js**

- Runs outside browser.
- Execute with:

```bash
node app.js
```

---

## Paths

| Path            | Meaning          |
| --------------- | ---------------- |
| `script.js`     | Current folder   |
| `./script.js`   | Current folder   |
| `../script.js`  | Parent folder    |
| `/js/script.js` | Website root     |
| `https://...`   | External website |

---

## Remember

- ✅ Use `<script>` to run JavaScript.
- ✅ Use `src` for external files.
- ✅ Scripts execute **top → bottom**.
- ✅ External scripts are **cached**.
- ❌ Don't mix `src` and inline code.
- ❌ `type` and `language` are obsolete (for normal JavaScript).

---

# JavaScript Code Structure — Revision Notes

## 1. Statement

- A **statement** is a command/instruction that performs an action.
- Multiple statements are usually separated by `;`.

```javascript
alert("Hello");
alert("World");
```

---

## 2. Semicolons (`;`)

- Marks the **end of a statement**.
- JavaScript can insert semicolons automatically (**ASI**), but **don't rely on it**.
- **Best Practice:** Always use semicolons.

---

## 3. Automatic Semicolon Insertion (ASI)

- JavaScript inserts semicolons **only when it can safely do so**.
- ASI **does not work in every case**.

✅ Works:

```javascript
alert("Hello");
alert("World");
```

❌ Can fail:

```javascript
alert("Hello")[(1, 2)].forEach(alert);
```

Interpreted as:

```javascript
alert("Hello")[(1, 2)].forEach(alert);
```

---

## 4. Incomplete Expressions

If an expression is incomplete, JavaScript **doesn't insert a semicolon**.

```javascript
alert(3 + 1 + 2);
```

Output:

```
6
```

---

## 5. Single-line Comment

Starts with `//`

```javascript
// This is a comment
alert("Hello");
```

---

## 6. Multi-line Comment

Starts with `/*` and ends with `*/`

```javascript
/*
This is
a comment
*/
```

---

## 7. Purpose of Comments

- Explain **what** the code does.
- Explain **why** it exists.
- Temporarily disable code.
- Improve readability.

---

## 8. Nested Comments

❌ Not allowed

```javascript
/*
   /* Nested */
*/
```

---

## 9. Comments & Production

- JavaScript ignores comments.
- Minifiers remove comments in production builds.
- No runtime performance impact.

---

## 10. Useful Shortcuts

| Action                     | Windows/Linux                         | Mac                                   |
| -------------------------- | ------------------------------------- | ------------------------------------- |
| Toggle single-line comment | `Ctrl + /`                            | `Cmd + /`                             |
| Toggle block comment       | `Ctrl + Shift + /` (editor-dependent) | `Cmd + Option + /` (editor-dependent) |

---

## Quick Rules

- ✅ A statement performs an action.
- ✅ End statements with `;`.
- ✅ ASI exists, but don't depend on it.
- ✅ `//` → Single-line comment.
- ✅ `/* ... */` → Multi-line comment.
- ❌ Nested block comments are invalid.
- ✅ Comments are ignored by JavaScript and removed during minification.

---

# 📝 Short & Crisp Revision Notes of Use Strict

## `"use strict"`

- Introduced in **ES5 (2009)**.
- Enables **modern, safer JavaScript behavior**.
- Helps avoid old language quirks.

---

## Syntax

```javascript
"use strict";
```

or

```javascript
"use strict";
```

---

## Placement

✅ Must be the **first statement**.

```javascript
"use strict";
```

Only **comments** may appear above it.

---

## Scope

- At top of script → Strict mode for the **entire script**.
- At top of a function → Strict mode for **that function only**.

---

## Rules

- ❌ Cannot be disabled (`"no use strict"` doesn't exist).
- ❌ Ignored if placed after executable code.

---

## Browser Console

- Console doesn't always use strict mode.
- Add `"use strict";` manually when testing.

---

## Modern JavaScript

- **Classes** → Strict mode automatically.
- **Modules** → Strict mode automatically.

---

## Best Practice

- ✅ Use `"use strict"` in normal scripts.
- ✅ No need in modules/classes.

---

## One-Line Summary

> **`"use strict"` is an ES5 directive that enables safer, modern JavaScript rules and must appear at the top of a script or function to take effect.**

# JavaScript Variables — Revision Notes

## Variable

- A **variable** is a **named storage** for data.
- Used to store and reuse information.

```javascript
let message = "Hello";
```

---

## Declaration Keywords

### `let`

- Modern way to declare variables.
- Value **can be changed**.

```javascript
let age = 20;
age = 21;
```

### `const`

- Declares a **constant**.
- Value **cannot be reassigned**.

```javascript
const PI = 3.14;
```

### `var`

- Old way of declaring variables.
- Avoid in modern JavaScript.

---

## Assignment

Use `=` to assign values.

```javascript
let name = "John";
```

---

## Copying Variables

```javascript
let a = "Hello";
let b = a;
```

Both variables contain `"Hello"`.

---

## Variable Naming Rules

✅ Allowed:

- Letters
- Digits (not first)
- `$`
- `_`

❌ Not Allowed:

- Start with a digit
- Hyphen (`-`)
- Reserved keywords (`let`, `return`, `class`, etc.)

---

## Naming Convention

Use **camelCase**.

```javascript
let firstName;
let shoppingCart;
```

---

## Case Sensitive

```javascript
apple;
APPLE;
```

These are **different variables**.

---

## Redeclaration

❌ Invalid

```javascript
let message = "Hi";
let message = "Hello";
```

A variable declared with `let` can only be declared **once in the same scope**.

---

## `use strict`

Without strict mode:

```javascript
num = 5;
```

Creates a variable (bad practice).

With strict mode:

```javascript
"use strict";

num = 5;
```

❌ Error: Variable not declared.

---

## Uppercase Constants

Use **UPPER_SNAKE_CASE** only for **hard-coded values**.

```javascript
const COLOR_RED = "#F00";
const MAX_USERS = 100;
```

Runtime constants use **camelCase**.

```javascript
const pageLoadTime = 2.3;
```

---

## Best Practices

- ✅ Use `let` for changing values.
- ✅ Use `const` whenever possible.
- ❌ Avoid `var`.
- ✅ Use meaningful names.
- ✅ Prefer one variable declaration per line.
- ❌ Don't reuse variables for different purposes.

---

## Quick Rules

- **`let`** → Mutable variable.
- **`const`** → Immutable binding (can't reassign).
- **`var`** → Legacy, avoid.
- Use **camelCase**.
- Variable names are **case-sensitive**.
- Use **descriptive names**.
- Declare variables before using them.
- Use **UPPER_SNAKE_CASE** only for hard-coded constants.
