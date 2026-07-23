# 6.11 Arrow Functions Revisited

Arrow functions are **syntactic sugar with lexical `this`**.

---

## No Own `this`

```javascript
const obj = {
  name: "John",

  say() {
    setTimeout(() => {
      console.log(this.name);
    }, 1000);
  },
};
```

Output

```
John
```

Arrow uses the surrounding `this`.

---

## Differences

| Normal Function            | Arrow Function               |
| -------------------------- | ---------------------------- |
| Own `this`                 | Lexical `this`               |
| Has `arguments`            | No own `arguments`           |
| Can be constructor         | Cannot be constructor        |
| Has `prototype`            | No `prototype`               |
| Can use `super` in methods | Inherits surrounding context |

---

## When to Use Arrow Functions

Good for:

- Callbacks
- Array methods (`map`, `filter`, `reduce`)
- Promise chains
- React components (in many cases)
- Functions that should inherit the surrounding `this`

Avoid when:

- Defining object methods that rely on their own `this`
- Constructor functions
- Methods that need `arguments`

---

# Summary Table

| Topic                        | Core Idea                                                                                                 |
| ---------------------------- | --------------------------------------------------------------------------------------------------------- |
| Recursion & Stack            | Functions can call themselves; each call occupies a stack frame until it returns.                         |
| Rest & Spread                | `...` collects arguments (rest) or expands iterables (spread).                                            |
| Scope & Closure              | Functions remember the lexical environment where they were created.                                       |
| `var`                        | Function-scoped, hoisted legacy declaration; prefer `let` and `const`.                                    |
| Global Object                | Environment-wide object (`globalThis`) exposing global APIs.                                              |
| Function Object & NFE        | Functions are callable objects with properties; named function expressions aid recursion/debugging.       |
| `new Function`               | Dynamically creates functions from strings; powerful but generally discouraged.                           |
| `setTimeout` & `setInterval` | Schedule one-time or repeated execution using the event loop.                                             |
| `call`, `apply`, `bind`      | Control a function's `this` value and argument passing.                                                   |
| Function Binding             | Permanently fixes `this` and supports partial application.                                                |
| Arrow Functions              | Concise syntax with lexical `this`, ideal for callbacks but not constructors or `this`-dependent methods. |
