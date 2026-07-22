# Introduction

- The programs in JS called scripts.
- It can run automatically as page loads.
- Javascript is executed on "Javascript Engines"
  V8 - Chrome, Opera, Edge
  SpiderMonkey - Firefox

# JavaScript Basics

---

# 1. Hello, World!

The first JavaScript program.

```javascript
console.log("Hello, World!");
```

Other output methods

```javascript
alert("Hello");
document.write("Hello");
```

### Purpose

- Test whether JavaScript is working.
- Learn basic syntax.
- Understand program execution.

---

# 2. Code Structure

A JavaScript program is made of **statements**.

```javascript
let age = 20;
console.log(age);
```

### Statements

Each instruction is a statement.

```javascript
let a = 5;
let b = 10;
```

### Semicolons

Optional in most places because of **Automatic Semicolon Insertion (ASI)**.

Recommended:

```javascript
let a = 5;
let b = 10;
```

### Comments

Single line

```javascript
// This is a comment
```

Multi-line

```javascript
/*
Multiple
Lines
*/
```

---

# 3. Strict Mode

```javascript
"use strict";
```

Enables a stricter version of JavaScript.

Benefits

- Prevents accidental global variables
- Throws more errors
- Makes code safer
- Easier to optimize

Example

Without strict mode

```javascript
x = 10;
```

Works (bad).

With strict mode

```javascript
"use strict";

x = 10;
```

Throws an error.

---

# 4. Variables

Variables store data.

Declaration

```javascript
let age = 20;
```

### Types of variable declaration

## let

Can change.

```javascript
let score = 10;
score = 20;
```

---

## const

Cannot be reassigned.

```javascript
const PI = 3.14;
```

---

## var

Old way.

```javascript
var name = "John";
```

Avoid using `var`.

---

Variable naming rules

- Can contain letters
- Digits
- \_
- $
- Cannot start with number

Good

```javascript
userName;
totalPrice;
```

Bad

```javascript
123abc
```

---

# 5. Data Types

JavaScript has two categories.

## Primitive

- Number
- String
- Boolean
- Null
- Undefined
- BigInt
- Symbol

Example

```javascript
let age = 21;
let name = "Alice";
let isAdmin = true;
let value = null;
let x;
```

---

## Object

Everything complex.

```javascript
let person = {
  name: "John",
  age: 20,
};
```

Arrays

```javascript
let numbers = [1, 2, 3];
```

Functions are also objects.

---

# 6. Interaction (alert, prompt, confirm)

### alert()

Displays message.

```javascript
alert("Welcome");
```

---

### prompt()

Takes user input.

```javascript
let name = prompt("Your name?");
```

Returns

- String
- null

---

### confirm()

Yes/No dialog.

```javascript
let result = confirm("Delete?");
```

Returns

- true
- false

---

# 7. Type Conversions

Automatic conversion is called **Implicit Coercion**.

Manual conversion is called **Explicit Conversion**.

---

## String()

```javascript
String(123);
```

Result

```
"123"
```

---

## Number()

```javascript
Number("45");
```

Result

```
45
```

---

## Boolean()

```javascript
Boolean(1);
```

Result

```
true
```

Falsy values

- 0
- ""
- null
- undefined
- NaN
- false

Everything else is truthy.

---

# 8. Basic Operators

Arithmetic

```javascript
+
-
*
/
%
**
```

Example

```javascript
5 + 3;
5 * 2;
10 % 3;
2 ** 4;
```

---

Assignment

```javascript
=
+=
-=
*=
/=
```

---

Unary

```javascript
++a;
a++;
--a;
```

---

# 9. Comparisons

Operators

```javascript
>
<
>=
<=
```

Equality

Loose equality

```javascript
==
```

Strict equality

```javascript
===
```

Difference

```javascript
5 == "5";
```

True

```javascript
5 === "5";
```

False

Always prefer

```javascript
===
```

---

# 10. Conditional Branching

## if

```javascript
if (age >= 18) {
  console.log("Adult");
}
```

---

## if else

```javascript
if (age >= 18) {
} else {
}
```

---

## else if

```javascript
if (score >= 90) {
} else if (score >= 70) {
} else {
}
```

---

## Ternary Operator

```javascript
condition ? value1 : value2;
```

Example

```javascript
let result = age >= 18 ? "Adult" : "Minor";
```

---

# 11. Logical Operators

AND

```javascript
&&
```

Both must be true.

---

OR

```javascript
||
```

At least one true.

---

NOT

```javascript
!
```

Reverse boolean.

---

Example

```javascript
if (age > 18 && citizen) {
}
```

---

# 12. Nullish Coalescing

Operator

```javascript
??
```

Returns first value that is **not null or undefined**.

```javascript
let name = userName ?? "Guest";
```

Difference

```javascript
0 || 100;
```

Returns

```
100
```

Because 0 is falsy.

```javascript
0 ?? 100;
```

Returns

```
0
```

Because 0 isn't null or undefined.

---

# 13. Loops

## while

```javascript
while (condition) {}
```

Example

```javascript
let i = 1;

while (i <= 5) {
  console.log(i);
  i++;
}
```

---

## do...while

Runs at least once.

```javascript
do {} while (condition);
```

---

## for

```javascript
for (let i = 0; i < 5; i++) {}
```

Structure

```
Initialization
Condition
Increment
```

---

Keywords

```javascript
break
continue
```

---

# 14. Switch Statement

Alternative to multiple if-else.

```javascript
switch (day) {
  case 1:
    console.log("Monday");
    break;

  case 2:
    console.log("Tuesday");
    break;

  default:
    console.log("Unknown");
}
```

Remember

Always use

```javascript
break;
```

unless intentional fall-through is desired.

---

# 15. Functions

Reusable block of code.

```javascript
function greet() {
  console.log("Hello");
}
```

Calling

```javascript
greet();
```

Parameters

```javascript
function add(a, b) {
  return a + b;
}
```

Return value

```javascript
let sum = add(2, 3);
```

---

# 16. Function Expressions

Functions stored inside variables.

```javascript
const greet = function () {
  console.log("Hello");
};
```

Anonymous function

```javascript
const add = function (a, b) {
  return a + b;
};
```

Difference

Function declarations are **hoisted**.

```javascript
hello();

function hello() {}
```

Works.

Function expressions are **not initialized until assignment**.

```javascript
hello();

const hello = function () {};
```

Throws an error.

---

# 17. Arrow Functions

Shorter syntax for writing functions.

Traditional

```javascript
function add(a, b) {
  return a + b;
}
```

Arrow

```javascript
const add = (a, b) => {
  return a + b;
};
```

Short form

```javascript
const add = (a, b) => a + b;
```

Single parameter

```javascript
const square = (x) => x * x;
```

No parameters

```javascript
const greet = () => "Hello";
```

### Characteristics

- Shorter syntax
- No own `this`
- Cannot be used as constructors
- Best for callbacks and functional programming

---
