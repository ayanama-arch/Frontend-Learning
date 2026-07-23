---

# 5.1 Methods of Primitives

## First Principle

JavaScript has **7 primitive data types**

```
String
Number
BigInt
Boolean
Undefined
Null
Symbol
```

Primitives are **not objects**.

Yet this works:

```javascript
let str = "hello";

console.log(str.toUpperCase());
```

How can a primitive call methods?

---

## The Problem

A primitive is simply a value.

```
"hello"
```

It has no properties.

So how does this work?

```javascript
str.length;
str.toUpperCase();
```

---

## The Hidden Process

Whenever you access a property or method,

```javascript
"hello".toUpperCase();
```

JavaScript secretly does this:

```
Primitive

↓

Temporary Wrapper Object

↓

Method Executes

↓

Wrapper Deleted
```

Internally

```javascript
new String("hello");
```

(Not exactly, but conceptually.)

Then

```javascript
wrapper.toUpperCase();
```

Returns

```
HELLO
```

Then wrapper disappears.

---

## Example

```javascript
let str = "ayan";

console.log(str.toUpperCase());
```

Output

```
AYAN
```

No object remains afterwards.

---

## Primitive Wrappers

| Primitive | Wrapper Object |
| --------- | -------------- |
| String    | String         |
| Number    | Number         |
| Boolean   | Boolean        |
| Symbol    | Symbol         |
| BigInt    | BigInt         |

---

## Why Wrapper Objects Exist

Imagine if every string needed an object.

```
Memory Waste

Slower

Extra Allocation
```

Instead JavaScript creates one **only when needed**.

---

## Important

Avoid manually creating wrappers.

Bad

```javascript
let str = new String("Hello");
```

Good

```javascript
let str = "Hello";
```

Reason:

```javascript
typeof new String("hello");
```

returns

```
object
```

while

```javascript
typeof "hello";
```

returns

```
string
```

---

## Null and Undefined

These have **no wrapper objects.**

```javascript
null.toString();
```

Error.

---
