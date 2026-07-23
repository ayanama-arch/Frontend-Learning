# 5.5 Array Methods

## Iteration

```javascript
forEach();
```

---

## Transformation

```javascript
map();
```

Returns new array.

```javascript
let doubled = arr.map((x) => x * 2);
```

---

## Filtering

```javascript
filter();
```

---

## Searching

```javascript
find();

findIndex();

includes();

indexOf();
```

---

## Reduction

```javascript
reduce();
```

Example

```javascript
let sum = arr.reduce((a, b) => a + b);
```

---

## Sorting

```javascript
sort();
```

Correct

```javascript
numbers.sort((a, b) => a - b);
```

---

## Reverse

```javascript
reverse();
```

---

## Flat

```javascript
flat();

flatMap();
```

---

## Copy

```javascript
Array.from();

Array.of();
```

---

## Mutating vs Non-mutating

| Mutates    | Doesn't Mutate |
| ---------- | -------------- |
| push       | map            |
| pop        | filter         |
| splice     | slice          |
| reverse    | concat         |
| sort       | toSorted()     |
| fill       | toReversed()   |
| copyWithin | toSpliced()    |

---

# 5.6 Iterables

## First Principle

Anything that can be used inside

```javascript
for...of
```

is iterable.

---

Examples

```javascript
Array;

String;

Map;

Set;
```

---

Example

```javascript
for (const c of "hello") {
  console.log(c);
}
```

---

## Symbol.iterator

Every iterable has

```javascript
Symbol.iterator;
```

which returns an iterator.

---

Iterator

```
next()

↓

{value, done}
```

---

Example

```javascript
const iterator = [1, 2][Symbol.iterator]();

iterator.next();
```

Returns

```javascript
{
    value:1,
    done:false
}
```

---

# 5.7 Map and Set

## Map

Stores

```
key → value
```

Unlike objects,

keys can be anything.

```javascript
let map = new Map();

map.set({}, "Object Key");
```

---

Methods

```
set()

get()

has()

delete()

clear()
```

---

## Set

Stores unique values.

```javascript
let set = new Set();

set.add(5);

set.add(5);
```

Only one remains.

---

Useful

```
Remove duplicates
```

```javascript
[...new Set(arr)];
```

---

# 5.8 WeakMap and WeakSet

These hold **weak references**.

Meaning

```
Garbage Collector
can remove entries automatically.
```

---

WeakMap

Keys must be objects.

```javascript
const wm = new WeakMap();

let user = {};

wm.set(user, "Admin");
```

---

When

```javascript
user = null;
```

Memory is freed.

---

Cannot

```
iterate

size

clear
```

---

Use Case

```
Private metadata

Caching

DOM elements
```

---
