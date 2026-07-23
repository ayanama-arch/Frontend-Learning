# 4.1 Objects

## Goal

Learn what objects are, why JavaScript needs them, and how they store data.

### Topics to Cover

### 1. Why Objects Exist

- Primitive values vs Objects
- Limitation of primitive values
- Real-world analogy (Person, Car, Book)

```javascript
const person = {
  name: "John",
  age: 25,
  city: "London",
};
```

---

### 2. What is an Object?

Definition

- Collection of key-value pairs
- Mutable
- Dynamic
- Stored by reference

Diagram

```
Object

↓

{
    key : value,
    key : value
}
```

---

### 3. Creating Objects

#### Object Literal

```javascript
const user = {
  name: "Alice",
};
```

#### Object Constructor

```javascript
const user = new Object();
```

---

### 4. Properties

Reading

```javascript
user.name;
```

Writing

```javascript
user.age = 30;
```

Deleting

```javascript
delete user.age;
```

Checking existence

```javascript
"name" in user;
```

---

### 5. Dot vs Bracket Notation

```javascript
user.name;
```

vs

```javascript
user["name"];
```

Dynamic keys

```javascript
const key = "name";

user[key];
```

---

### 6. Computed Properties

```javascript
let field = "age";

const user = {
  [field]: 25,
};
```

---

### 7. Property Names

Numbers

```javascript
{
    1: "One"
}
```

Strings

Symbols

Reserved keywords

---

### 8. Iterating

```javascript
for (let key in user)
```

---

### 9. Object Methods Preview

```javascript
const user = {
  greet() {},
};
```

---

### Practical Exercises

Build

- Student
- Product
- Employee
- Phone Specification
- Course Object

---
