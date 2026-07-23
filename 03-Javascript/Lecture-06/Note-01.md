# Chapter 7 — Object Properties Configuration

---

# 7.1 Property Flags and Descriptors

---

# First Principle

When we create an object property,

```javascript
const user = {
  name: "Ayan",
};
```

it looks like the property stores only a value.

```
name

↓

"Ayan"
```

But internally every property stores **much more information**.

Think of every property as an object like this:

```
Property

├── value
├── writable
├── enumerable
└── configurable
```

These hidden settings are called **Property Descriptors**.

---

# Internal Representation

Internally,

```javascript
const user = {
  name: "Ayan",
};
```

actually behaves like

```javascript
{
    value: "Ayan",
    writable: true,
    enumerable: true,
    configurable: true
}
```

The descriptor is **metadata** about the property.

---

# What is a Property Descriptor?

A property descriptor is an object describing a property's behavior.

Retrieve it using

```javascript
Object.getOwnPropertyDescriptor();
```

Example

```javascript
const user = {
  name: "Ayan",
};

console.log(Object.getOwnPropertyDescriptor(user, "name"));
```

Output

```javascript
{
    value: "Ayan",
    writable: true,
    enumerable: true,
    configurable: true
}
```

---

# The Three Flags

---

## 1. writable

Determines whether the property's value can be changed.

```
true

↓

Modification Allowed
```

```
false

↓

Read Only
```

Example

```javascript
const user = {};

Object.defineProperty(user, "id", {
  value: 101,
  writable: false,
});

user.id = 500;

console.log(user.id);
```

Output

```
101
```

Nothing changes.

---

## 2. enumerable

Determines whether the property appears during iteration.

Example

```javascript
const user = {};

Object.defineProperty(user, "password", {
  value: "secret",
  enumerable: false,
});
```

Now

```javascript
console.log(Object.keys(user));
```

Output

```javascript
[];
```

Even though

```javascript
console.log(user.password);
```

works perfectly.

---

Example

```javascript
for (let key in user) {
  console.log(key);
}
```

Nothing prints.

---

## 3. configurable

Controls whether the property can be changed or deleted later.

```
true

↓

Descriptor can change
```

```
false

↓

Descriptor locked forever
```

Example

```javascript
const user = {};

Object.defineProperty(user, "id", {
  value: 1,
  configurable: false,
});
```

Now

```javascript
delete user.id;
```

Fails.

Trying

```javascript
Object.defineProperty(user, "id", {
  enumerable: false,
});
```

also fails.

---

# defineProperty()

Creates a property with custom descriptors.

Syntax

```javascript
Object.defineProperty(object, property, descriptor);
```

Example

```javascript
const user = {};

Object.defineProperty(user, "name", {
  value: "Ayan",
  writable: false,
  enumerable: true,
  configurable: false,
});
```

---

# defineProperties()

Create many properties simultaneously.

```javascript
Object.defineProperties(user, {
  name: {
    value: "Ayan",
  },

  age: {
    value: 23,
  },
});
```

---

# getOwnPropertyDescriptors()

Returns descriptors of every property.

```javascript
console.log(Object.getOwnPropertyDescriptors(user));
```

Useful for cloning objects while preserving descriptors.

---

# Object.freeze()

Makes an object immutable.

```
Cannot

Change

Delete

Add
```

Example

```javascript
const user = {
  name: "Ayan",
};

Object.freeze(user);

user.name = "John";

console.log(user.name);
```

Output

```
Ayan
```

---

# Object.seal()

Allows

```
Modify Existing Values

✓
```

Prevents

```
Delete

Add
```

---

# Object.preventExtensions()

Only prevents

```
Adding New Properties
```

Existing ones remain writable and configurable (unless already changed).

---

# Comparison

| Method            | Add | Delete | Modify                   |
| ----------------- | --- | ------ | ------------------------ |
| preventExtensions | ❌  | ✅     | ✅                       |
| seal              | ❌  | ❌     | ✅                       |
| freeze            | ❌  | ❌     | ❌ (for data properties) |

---

# Cloning With Descriptors

Normal cloning

```javascript
const clone = {
  ...user,
};
```

copies only values.

Descriptor information is lost.

Correct way

```javascript
const clone = Object.defineProperties(
  {},
  Object.getOwnPropertyDescriptors(user),
);
```

---

# Why Property Descriptors Exist

JavaScript uses descriptors everywhere.

Example

```javascript
Math.PI;
```

cannot be modified.

Why?

Because internally

```javascript
{
    value:3.1415926535,
    writable:false,
    configurable:false
}
```

---
