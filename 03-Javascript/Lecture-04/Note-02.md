# 5.2 Numbers

JavaScript has only **one numeric type**

```
Number
```

Unlike C++

```
int
float
double
long
short
```

JavaScript combines all into one.

---

## IEEE-754

Numbers are stored using

```
64 bits
```

Layout

```
1 bit    Sign

11 bits  Exponent

52 bits  Fraction
```

---

## Integer Range

Safe Integer

```javascript
Number.MAX_SAFE_INTEGER;
```

```
9007199254740991
```

Beyond this

```
Precision Loss
```

Example

```javascript
9007199254740992 === 9007199254740993;
```

returns

```
true
```

---

## BigInt

For huge integers

```javascript
let x = 123456789012345678901234567890n;
```

Notice

```
n
```

---

## Special Numeric Values

### Infinity

```javascript
1 / 0;
```

```
Infinity
```

---

### -Infinity

```javascript
-1 / 0;
```

---

### NaN

Means

```
Not a Number
```

Example

```javascript
"abc" * 5;
```

Output

```
NaN
```

---

## Checking Numbers

```javascript
Number.isNaN();
```

```javascript
Number.isFinite();
```

Example

```javascript
Number.isNaN(NaN);
```

```
true
```

---

## Parsing

```javascript
parseInt("25px");
```

```
25
```

```javascript
parseFloat("10.5kg");
```

```
10.5
```

---

## Rounding

```javascript
Math.floor();
Math.ceil();
Math.round();
Math.trunc();
```

---

## Random

```javascript
Math.random();
```

Returns

```
0 <= x < 1
```

---

# 5.3 Strings

Strings are immutable.

```javascript
let str = "hello";
```

You cannot change

```
str[0]
```

---

## Access

```javascript
str[0];

str.at(0);

str.at(-1);
```

Example

```javascript
"hello".at(-1);
```

```
o
```

---

## Common Methods

Uppercase

```javascript
toUpperCase();
```

Lowercase

```javascript
toLowerCase();
```

Search

```javascript
includes();

startsWith();

endsWith();
```

Slice

```javascript
slice();

substring();
```

Replace

```javascript
replace();

replaceAll();
```

Split

```javascript
split();
```

Join

```javascript
array.join();
```

Trim

```javascript
trim();
```

Repeat

```javascript
repeat();
```

---

## Template Literals

```javascript
let name = "Ayan";

console.log(`Hello ${name}`);
```

---

## Unicode

JavaScript stores strings as

```
UTF-16
```

Not ASCII.

---

# 5.4 Arrays

Arrays are ordered collections.

```javascript
let fruits = ["Apple", "Banana"];
```

---

## Dynamic

Arrays can grow.

```javascript
fruits.push("Orange");
```

---

## Heterogeneous

```javascript
[1, "hello", true, {}, []];
```

Allowed.

---

## Length

```javascript
arr.length;
```

---

## Common Operations

```
push()

pop()

shift()

unshift()

splice()

slice()

concat()
```

---

## Sparse Arrays

```javascript
let arr = [];

arr[100] = "Hello";
```

Length becomes

```
101
```

---

## Array vs Object

Array

```
Ordered

Numeric Index
```

Object

```
Named Keys
```

---
