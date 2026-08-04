# JavaScript Conditional Branching (`if`, `else`, `?`) — Quick Revision

Based on your notes.

---

## `if`

Executes code if the condition is **true**.

```js
if (condition) {
  // code
}
```

---

## `if...else`

Runs one block if true, another if false.

```js
if (condition) {
  // true block
} else {
  // false block
}
```

---

## `else if`

Checks multiple conditions.

```js
if (condition1) {
    ...
} else if (condition2) {
    ...
} else {
    ...
}
```

---

## Truthy & Falsy

###### Falsy (6)

```js
false;
0;
("");
null;
undefined;
NaN;
```

Everything else is **truthy**.

---

## Ternary Operator (`?`)

Short form of `if...else`.

```js
condition ? value1 : value2;
```

Example

```js
let access = age >= 18 ? true : false;
```

Even shorter:

```js
let access = age >= 18;
```

---

## Multiple `?`

Can replace multiple `else if`s.

```js
let msg =
  age < 3
    ? "Baby"
    : age < 18
      ? "Hello"
      : age < 100
        ? "Greetings"
        : "Unusual age";
```

---

## When to Use `?`

✅ Use when **returning/assigning a value**.

```js
let status = age >= 18 ? "Adult" : "Minor";
```

❌ Don't use it to execute large code blocks.

```js
// Avoid
condition ? doThis() : doThat();
```

Use `if...else` instead.

---

## Best Practices ⭐

- Always use `{}` with `if` blocks.
- Use `if...else` for **executing code**.
- Use `?` for **assigning values**.
- Avoid long nested ternary expressions if readability suffers.

---

## Must Remember ⭐

- `if` → Execute code when condition is true.
- `else` → Runs when `if` is false.
- `else if` → Check multiple conditions.
- `?` → Short form of `if...else` for **returning values**.
- **Falsy values:** `false`, `0`, `""`, `null`, `undefined`, `NaN`.
- Everything else is **truthy**.
- Prefer `if...else` over complex nested ternaries for readability.

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

---

# JavaScript Nullish Coalescing (`??`) — Quick Revision

Based on your notes.

---

## Nullish Coalescing (`??`)

Returns the **first defined value**.

Defined = **not `null` and not `undefined`**.

```js
a ?? b;
```

- If `a` is **not null/undefined** → returns `a`.
- Otherwise → returns `b`.

---

## Common Use

Default values.

```js
let user = null;

user ?? "Anonymous"; // "Anonymous"
```

```js
let user = "John";

user ?? "Anonymous"; // "John"
```

---

## Multiple `??`

Returns the **first defined value**.

```js
firstName ?? lastName ?? nickName ?? "Anonymous";
```

---

## `??` vs `||`

| `??`                             | `                       |     | `   |
| -------------------------------- | ----------------------- | --- | --- |
| First **defined** value          | First **truthy** value  |
| Only checks `null` & `undefined` | Checks all falsy values |

Example

```js
let height = 0;

height || 100; // 100 ❌
height ?? 100; // 0 ✅
```

> ⭐ Use `??` when `0`, `false`, or `""` are valid values.

---

## Precedence

- Same precedence as `||`.
- Lower than `*`, `+`, etc.

Use parentheses:

```js
(height ?? 100) * (width ?? 50);
```

---

## Mixing with `&&` or `||`

❌ Not allowed without parentheses.

```js
1 && 2 ?? 3   // Syntax Error
```

✅ Correct

```js
(1 && 2) ?? 3;
```

---

## Best Practice ⭐

- Use `??` for default values.
- Use `||` when any **falsy** value should trigger the fallback.
- Add parentheses when combining `??` with other operators.

---

## Must Remember ⭐

- `??` → Returns the **first defined** value.
- Defined = **not `null` and not `undefined`**.
- `||` → First **truthy** value.
- `0`, `false`, `""` are **kept** by `??`.
- `0`, `false`, `""` are **replaced** by `||`.
- Don't mix `??` with `&&` or `||` without parentheses.
- Use parentheses in complex expressions.
