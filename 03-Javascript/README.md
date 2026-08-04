# JavaScript Logical Operators (`||`, `&&`, `!`) — Quick Revision

Based on your notes.

---

## Logical Operators

| Operator | Meaning |     |     |
| -------- | ------- | --- | --- |
| `        |         | `   | OR  |
| `&&`     | AND     |     |     |
| `!`      | NOT     |     |     |

> They work with **any data type**, not just booleans.

---

## OR (`||`)

Returns the **first truthy value**, or the **last value** if all are falsy.

```js
a || b;
```

Examples

```js
1 || 0; // 1
null || "Hello"; // "Hello"
null || 0 || 5; // 5
undefined || null || 0; // 0
```

###### Common Use

Default value:

```js
let name = firstName || lastName || "Anonymous";
```

###### Short-Circuit

Stops at the **first truthy value**.

```js
true || alert("Won't run");
false || alert("Runs");
```

---

## AND (`&&`)

Returns the **first falsy value**, or the **last value** if all are truthy.

```js
a && b;
```

Examples

```js
1 && 5; // 5
1 && 0; // 0
null && 5; // null
1 && 2 && 3; // 3
1 && 2 && null; // null
```

###### Short-Circuit

Stops at the **first falsy value**.

---

## Precedence

```text
!   Highest
&&
||  Lowest
```

Example

```js
(a && b) || c;
```

is evaluated as

```js
(a && b) || c;
```

---

## NOT (`!`)

Reverses a boolean value.

```js
!true; // false
!false; // true
!0; // true
```

---

## Double NOT (`!!`)

Converts any value to a boolean.

```js
!!"Hello"; // true
!!0; // false
!!null; // false
```

Equivalent to:

```js
Boolean(value);
```

---

## Best Practices ⭐

- `||` → Default/fallback values.
- `&&` → Check multiple conditions.
- `!` → Negate a condition.
- `!!` → Convert to boolean.
- Prefer `if` over clever uses of `&&` or `||` for executing code.

---

## Must Remember ⭐

- `||` → **First truthy**, otherwise **last value**.
- `&&` → **First falsy**, otherwise **last value**.
- Both use **short-circuit evaluation**.
- `!` reverses a boolean.
- `!!value` = `Boolean(value)`.
- Precedence: **`!` > `&&` > `||`**.
