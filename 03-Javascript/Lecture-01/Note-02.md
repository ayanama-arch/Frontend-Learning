# JavaScript Data Types — One-Page Quick Revision

### JavaScript

- **Dynamically Typed** → Variables can hold any data type.

```js
let x = "Hello";
x = 100;
```

---

## 8 Data Types

### Primitive (7)

1. **Number** → Integers & decimals
   - Special values: `Infinity`, `-Infinity`, `NaN`
   - `NaN` is **sticky** (`NaN + 1 → NaN`)

2. **BigInt** → Very large integers

```js
12345678901234567890n;
```

- Safe Number range: **±(2^53 − 1)**

3. **String** → Text

- Quotes: `" "`, `' '`, `` ` ` ``
- Only **backticks** support `${}` interpolation.

4. **Boolean**

```js
true;
false;
```

5. **null**

- Intentional empty/unknown value.

6. **undefined**

- Variable declared but not assigned.

7. **Symbol**

- Unique identifiers.

---

### Non-Primitive (1)

8. **Object**

- Stores collections of data.
- Arrays, Functions, Dates, etc., are objects.

---

## `typeof`

```js
typeof 5; // "number"
typeof 10n; // "bigint"
typeof "Hi"; // "string"
typeof true; // "boolean"
typeof undefined; // "undefined"
typeof Symbol(); // "symbol"
typeof {}; // "object"
typeof null; // "object" ❌ (historical bug)
typeof alert; // "function"
```

---

## `null` vs `undefined`

| `null`            | `undefined`  |
| ----------------- | ------------ |
| Intentional empty | Not assigned |

---

## Must Remember ⭐

- **8 data types** → 7 Primitive + 1 Object
- JavaScript is **dynamically typed**
- `NaN` spreads through calculations.
- `BigInt` ends with **`n`**.
- Only **backticks** support `${}`.
- No separate **char** type.
- `typeof null` → `"object"` (**bug**).
- `typeof` always returns a **string**.

# Interaction (`alert`, `prompt`, `confirm`) — Quick Revision

## `alert()`

- Shows a **message**.
- Has only **OK** button.
- Returns **nothing (`undefined`)**.

```js
alert("Hello");
```

---

## `prompt()`

- Takes user input.
- **Syntax:**

```js
prompt(message, defaultValue);
```

- Returns:
  - User input → **String**
  - Cancel/Esc → **null**

```js
let age = prompt("Age?", 18);
```

> 💡 `defaultValue` is **optional**.

---

## `confirm()`

- Asks a **Yes/No** question.
- Returns:
  - **true** → OK
  - **false** → Cancel/Esc

```js
let ok = confirm("Are you sure?");
```

---

## Modal Windows

- Pause JavaScript execution.
- User **can't interact** with the page until closed.

---

## Limitations

- Browser controls **position** and **appearance**.
- Cannot customize them.

---

## Quick Comparison

| Method      | Purpose          | Returns           |
| ----------- | ---------------- | ----------------- |
| `alert()`   | Show message     | `undefined`       |
| `prompt()`  | Get user input   | `String` / `null` |
| `confirm()` | Ask confirmation | `true` / `false`  |

### Remember ⭐

- `alert` → Display message.
- `prompt` → Input from user.
- `confirm` → Boolean confirmation.
- All are **modal** (block interaction until closed).

# Type Conversions — Quick Revision

## Type Conversion

- JavaScript automatically converts values when needed (**implicit conversion**).
- You can also convert values manually (**explicit conversion**).

---

## 1. String Conversion

Convert using:

```js
String(value);
```

Examples:

```js
String(true); // "true"
String(null); // "null"
String(123); // "123"
```

**Used when:** Displaying/outputting values (`alert`, etc.)

---

## 2. Number Conversion

Convert using:

```js
Number(value);
```

Examples:

```js
Number("123"); // 123
Number("123abc"); // NaN
Number(true); // 1
Number(false); // 0
```

### Number Conversion Rules

| Value       | Result |
| ----------- | ------ |
| `undefined` | `NaN`  |
| `null`      | `0`    |
| `true`      | `1`    |
| `false`     | `0`    |
| `""`        | `0`    |
| `"123"`     | `123`  |
| `"123abc"`  | `NaN`  |

**Notes**

- Leading/trailing spaces are ignored.
- Invalid numbers → `NaN`.

---

## 3. Boolean Conversion

Convert using:

```js
Boolean(value);
```

### Falsy Values (Only 6)

```js
false;
0;
("");
null;
undefined;
NaN;
```

Everything else is **truthy**.

Examples:

```js
Boolean(1); // true
Boolean("Hi"); // true
Boolean([]); // true
Boolean({}); // true
Boolean("0"); // true
Boolean(" "); // true
```

---

# ⚠️ Common Mistakes

```js
Number(undefined); // NaN
Number(null); // 0

Boolean("0"); // true
Boolean(" "); // true
```

- `"0"` is **true** (non-empty string).
- `" "` (spaces only) is also **true**.

---

# Must Remember ⭐

- `String(value)` → Convert to string.
- `Number(value)` → Convert to number.
- `Boolean(value)` → Convert to boolean.
- **Falsy values:** `false`, `0`, `""`, `null`, `undefined`, `NaN`.
- Everything else is **truthy**.
- `null → 0`, but `undefined → NaN`.
- `"0"` and `" "` are **truthy**, not falsy.
