# 4.2 Object References & Copying

## Goal

Understand that **objects are copied by reference**, not by value.

---

### 1. Primitive Copy

```javascript
let a = 5;
let b = a;
```

Memory

```
a → 5
b → 5
```

Independent.

---

### 2. Object Copy

```javascript
let a = {
  name: "John",
};

let b = a;
```

Memory

```
a ─────┐
       │
       ▼
    Object

b ─────┘
```

---

### 3. Mutation

```javascript
b.name = "Alice";
```

Both change.

---

### 4. Equality

```javascript
{} == {}
```

False

Why?

Different memory addresses.

---

### 5. Shallow Copy

Spread

```javascript
const copy = {
  ...user,
};
```

Object.assign

```javascript
Object.assign({}, user);
```

---

### 6. Deep Copy

Nested object problem

```javascript
const user = {
  address: {
    city: "Delhi",
  },
};
```

Spread fails.

Solutions

- structuredClone()
- lodash cloneDeep()
- JSON stringify (limitations)

---

### 7. Nested Objects

Memory diagrams.

---

### Exercises

Implement

- Shopping Cart
- Employee
- Deep Copy examples

---

# 4.3 Garbage Collection

## Goal

Understand memory management.

---

### Topics

What is Memory?

Heap

Stack

Allocation

Reachability

Reference counting (history)

Mark and Sweep algorithm

Garbage Collector

Memory Leaks

---

### Example

```javascript
let obj = {
  name: "John",
};

obj = null;
```

GC can reclaim.

---

### Circular References

Why JS handles them.

---

### Common Memory Leaks

Timers

DOM references

Global variables

Closures

Detached DOM

---

### Best Practices

Avoid globals

Remove listeners

Clear intervals

---
