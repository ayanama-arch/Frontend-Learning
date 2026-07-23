# Chapter 6 — Advanced Working with Functions

---

# 6.1 Recursion and Stack

---

## First Principle

Normally a function solves a problem by **calling another function**.

Sometimes a function solves a problem by **calling itself**.

That is called **recursion**.

```
Problem

↓

Function

↓

Same Function

↓

Same Function

↓

Base Case

↓

Return Back
```

---

## Why Recursion Exists

Many problems naturally contain **smaller versions of themselves.**

Examples

```
Folder contains folders

Tree contains branches

Comment contains replies

DOM contains elements

JSON contains objects inside objects
```

Recursion follows this structure naturally.

---

## Structure of Every Recursive Function

Every recursive function has two parts.

```
Base Case

↓

Recursive Case
```

Example

```javascript
function countdown(n) {
  if (n === 0) return;

  console.log(n);

  countdown(n - 1);
}

countdown(5);
```

Output

```
5
4
3
2
1
```

---

## Call Stack

Whenever a function is called,

JavaScript pushes it onto the **Call Stack.**

Think of it as a stack of plates.

```
Top

countdown(1)

countdown(2)

countdown(3)

countdown(4)

countdown(5)

Bottom
```

Each function waits until the next one finishes.

Then JavaScript pops them one by one.

---

## Factorial Example

```
5!

↓

5 × 4!

↓

5 × 4 × 3!

↓

5 × 4 × 3 × 2!

↓

5 × 4 × 3 × 2 × 1
```

Code

```javascript
function factorial(n) {
  if (n === 1) return 1;

  return n * factorial(n - 1);
}
```

---

## Stack Overflow

If recursion never ends,

```
function hello() {
    hello();
}
```

Eventually

```
Maximum Call Stack Size Exceeded
```

---

## Tail Recursion

Some languages optimize

```
return recurse();
```

JavaScript engines generally **do not guarantee tail-call optimization**, so deep recursion can still overflow the stack.

---

## Recursion vs Loop

| Loop                         | Recursion                                    |
| ---------------------------- | -------------------------------------------- |
| Uses iteration               | Uses function calls                          |
| Faster                       | Often easier to express recursive structures |
| Constant memory              | Uses stack memory                            |
| Better for simple repetition | Better for trees, graphs, nested data        |

---
