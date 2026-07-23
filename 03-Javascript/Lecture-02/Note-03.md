# 4.4 Object Methods & "this"

## Goal

Understand functions inside objects.

---

### Topics

Method

```javascript
const user = {
  sayHi() {},
};
```

---

### this keyword

```javascript
const user = {
  name: "John",

  greet() {
    console.log(this.name);
  },
};
```

---

### Dynamic this

Depends on caller.

---

### Method Borrowing

```javascript
obj2.sayHi = obj1.sayHi;
```

---

### Arrow Function

Why

```
this
```

behaves differently.

---

### Losing this

```javascript
const fn = user.sayHi;

fn();
```

---

### bind()

call()

apply()

---

### Chaining

```javascript
calculator.add().subtract().multiply();
```

---

Exercises

Calculator

Bank Account

Todo App

---

# 4.5 Constructor Functions & new

## Goal

Create multiple objects.

---

### Why Constructors?

Avoid duplication.

---

### Constructor Function

```javascript
function User(name) {
  this.name = name;
}
```

---

### new Operator

Steps

```
new

↓

Create object

↓

Bind this

↓

Execute

↓

Return object
```

---

### instanceof

---

### Constructor Return Rules

---

### Capitalized Names

Convention

---

### Classes Preview

Difference

```
Constructor

↓

Class
```

---

Exercises

Book

Car

Employee

Phone

---

# 4.6 Optional Chaining (?.)

## Goal

Safely access nested data.

---

### Problem

```javascript
user.address.city;
```

If

```
address == undefined
```

↓

Crash.

---

### Solution

```javascript
user?.address?.city;
```

---

### Forms

Property

```javascript
obj?.name;
```

---

Method

```javascript
obj?.sayHi?.();
```

---

Array

```javascript
arr?.[0];
```

---

### Nullish Coalescing

Combine

```javascript
user?.name ?? "Guest";
```

---

### Difference

```
&&

vs

?.
```

---

Exercises

API Responses

Optional Config

Nested JSON

---
