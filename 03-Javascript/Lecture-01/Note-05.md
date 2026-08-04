# JavaScript Quick Revision Notes

---

# 1. Loops (`while` & `for`)

### `while`

- Repeats while condition is `true`.
- Best when number of iterations is unknown.

```js
while (condition) {
  // code
}
```

### `for`

- Best when iteration count is known.

```js
for (init; condition; update) {
  // code
}
```

### Loop Keywords

- `break` → Exit loop.
- `continue` → Skip current iteration.

⭐ **Remember**

- `while` → Unknown iterations.
- `for` → Known iterations.

---

# 2. `switch`

Used instead of multiple `if...else if`.

```js
switch (value) {
    case x:
        ...
        break;
    default:
        ...
}
```

- Uses **strict equality (`===`)**.
- `break` prevents fall-through.
- `default` runs if no case matches.

⭐ **Remember**

- Always use `break`.
- `default` is optional.

---

# 3. Functions

Reusable block of code.

```js
function greet(name) {
  return `Hello ${name}`;
}
```

- Can have parameters.
- Can return a value using `return`.
- Executes only when called.

⭐ **Remember**

- `return` ends the function.
- Functions are first-class objects.

---

# 4. Function Expressions

Function stored in a variable.

```js
const greet = function (name) {
  return `Hello ${name}`;
};
```

- Can be anonymous or named.
- Created when execution reaches it.
- Useful for callbacks.

⭐ **Remember**

- Stored in variables.
- No hoisting like function declarations.

---

# 5. Arrow Functions

Shorter syntax for functions.

```js
const greet = (name) => {
  return `Hello ${name}`;
};
```

Single expression:

```js
const square = (x) => x * x;
```

### Characteristics

- Short syntax.
- Implicit return (single expression).
- No own `this`.
- Cannot be used as constructors (`new`).

⭐ **Remember**

- Best for short functions & callbacks.
- Avoid when you need your own `this`.
