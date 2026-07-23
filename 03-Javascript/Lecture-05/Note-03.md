# 6.4 The Old "var"

Before ES6

```
var
```

was the only variable keyword.

---

## Differences

| var                                                             | let                                                             |
| --------------------------------------------------------------- | --------------------------------------------------------------- |
| Function scope                                                  | Block scope                                                     |
| Can redeclare                                                   | Cannot redeclare                                                |
| Hoisted                                                         | Hoisted (temporal dead zone prevents use before initialization) |
| Global `var` becomes a property of the global object in scripts | `let` does not                                                  |

---

Example

```javascript
if (true) {
  var x = 5;
}

console.log(x);
```

prints

```
5
```

---

But

```javascript
if (true) {
  let x = 5;
}

console.log(x);
```

Error.

---

## Hoisting

```javascript
console.log(a);

var a = 5;
```

prints

```
undefined
```

because

JavaScript behaves like

```javascript
var a;

console.log(a);

a = 5;
```

---

# 6.5 Global Object

Every JavaScript environment has one global object.

Browser

```
window
```

Workers

```
self
```

Modern standard

```
globalThis
```

Node.js

```
global
```

---

## Why Global Object Exists

It stores

```
Global Variables

Timers

Console

Math

JSON

setTimeout()

fetch()
```

---

Example

```javascript
console.log(globalThis.Math);
```

---

Browser

```javascript
window.alert("Hello");
```

---
