# 5.9 Object.keys(), values(), entries()

Suppose

```javascript
const user = {
  name: "Ayan",
  age: 22,
};
```

---

Keys

```javascript
Object.keys(user);
```

```
["name","age"]
```

---

Values

```javascript
Object.values(user);
```

```
["Ayan",22]
```

---

Entries

```javascript
Object.entries(user);
```

```
[
 ["name","Ayan"],
 ["age",22]
]
```

Useful with

```javascript
for (const [k,v] of Object.entries(user))
```

---

# 5.10 Destructuring Assignment

Extract values elegantly.

---

Array

```javascript
const [a, b] = [10, 20];
```

---

Object

```javascript
const { name, age } = user;
```

---

Rename

```javascript
const { name: username } = user;
```

---

Default

```javascript
const { country = "India" } = user;
```

---

Rest

```javascript
const [first, ...rest] = arr;
```

---

Nested

```javascript
const {
  address: { city },
} = obj;
```

---

# 5.11 Date and Time

Create

```javascript
new Date();
```

---

Timestamp

```javascript
Date.now();
```

Milliseconds since

```
Jan 1 1970 UTC
```

---

Methods

```
getFullYear()

getMonth()

getDate()

getDay()

getHours()

getMinutes()

getSeconds()
```

---

Formatting

```javascript
date.toLocaleDateString();

date.toLocaleTimeString();

date.toISOString();
```

---

Parsing

```javascript
new Date("2026-07-23");
```

---

Difference

```javascript
const diff = end - start;
```

Returns milliseconds.

---
