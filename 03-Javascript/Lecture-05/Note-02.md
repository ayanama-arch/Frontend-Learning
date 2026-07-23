# 6.2 Rest Parameters and Spread Syntax

Although they look identical (`...`), **rest** and **spread** do opposite jobs.

```
Rest

Many values

↓

One Array
```

```
Spread

One Array

↓

Many Values
```

---

## Rest Parameters

Collects remaining arguments.

```javascript
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b, 0);
}
```

Calling

```javascript
sum(1, 2, 3, 4);
```

means

```
numbers

↓

[1,2,3,4]
```

---

## Spread Syntax

Expands iterable values.

```javascript
const arr = [1, 2, 3];

console.log(...arr);
```

becomes

```
1 2 3
```

---

## Copy Arrays

```javascript
const copy = [...arr];
```

---

## Merge Arrays

```javascript
const both = [...a, ...b];
```

---

## Copy Objects

```javascript
const user2 = {
  ...user,
};
```

---

## Override Properties

```javascript
const user = {
  name: "John",
  age: 20,
};

const updated = {
  ...user,
  age: 25,
};
```

---

# 6.3 Variable Scope, Closure

This is **the most important JavaScript concept**.

Everything in React depends on closures.

---

## Scope

Scope determines

```
Where variables are visible.
```

---

Example

```javascript
let x = 10;

function hello() {
  console.log(x);
}
```

The function can access

```
Outer Scope
```

---

## Lexical Scope

JavaScript uses

```
Where function is written

NOT

Where function is called
```

Example

```javascript
let x = 5;

function a() {
  console.log(x);
}
```

Even if another function has

```javascript
let x = 100;
```

`a()` still prints

```
5
```

because of where it was created.

---

## Closure

Definition

> A closure is a function together with the lexical environment in which it was created.

---

Example

```javascript
function counter() {
  let count = 0;

  return function () {
    count++;

    return count;
  };
}

const c = counter();

console.log(c());
console.log(c());
console.log(c());
```

Output

```
1

2

3
```

---

Why?

Because

```
count

doesn't disappear.
```

The inner function remembers it.

---

## Memory Picture

```
counter()

↓

count = 0

↓

return function

↓

counter finished

↓

count still alive

↓

Closure
```

---

## Real Uses

```
React Hooks

Event Listeners

Memoization

Private Variables

Currying

Module Pattern
```

---
