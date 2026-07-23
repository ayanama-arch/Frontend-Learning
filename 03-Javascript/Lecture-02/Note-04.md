# 4.7 Symbol Type

## Goal

Understand JavaScript's unique primitive.

---

### Primitive Types Review

```
String

Number

Boolean

Null

Undefined

BigInt

Symbol
```

---

### Creating Symbol

```javascript
const id = Symbol();
```

---

### Description

```javascript
Symbol("id");
```

---

### Uniqueness

```javascript
Symbol() === Symbol();
```

False.

---

### Object Keys

```javascript
const id = Symbol();

user[id] = 10;
```

---

### Hidden Properties

---

### Global Symbol Registry

```javascript
Symbol.for();
```

---

### Symbol.keyFor()

---

### Well-known Symbols

```
Symbol.iterator

Symbol.toPrimitive

Symbol.asyncIterator

Symbol.hasInstance
```

---

Exercises

Private IDs

Iterators

---

# 4.8 Object to Primitive Conversion

## Goal

Understand how objects behave in expressions.

---

### Problem

```javascript
const obj = {};

obj + 5;
```

How?

---

### Conversion Hints

```
String

Number

Default
```

---

### toString()

```javascript
obj.toString();
```

---

### valueOf()

```javascript
obj.valueOf();
```

---

### Symbol.toPrimitive

```javascript
obj[Symbol.toPrimitive];
```

---

### Examples

```javascript
String(user);
```

```javascript
Number(user);
```

```javascript
user + "";
```

```javascript
user + 10;
```

---

### Custom Conversion

```javascript
const money = {
  amount: 100,

  [Symbol.toPrimitive](hint) {
    return this.amount;
  },
};
```

---

### Comparison

```
==

===

<

>

+
```

How conversion occurs.

---

Exercises

Money Object

Temperature Object

Fraction Object

---

# Recommended Learning Order

```
Objects
│
├── Object Structure
│
├── References & Copying
│
├── Garbage Collection
│
├── Methods & this
│
├── Constructor Functions
│
├── Optional Chaining
│
├── Symbol
│
└── Object to Primitive Conversion
```
