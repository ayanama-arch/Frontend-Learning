# 6.6 Function Object, NFE

Functions are objects.

```
Function

↓

Object

↓

Callable
```

---

Example

```javascript
function hello() {}

hello.language = "JS";

console.log(hello.language);
```

Output

```
JS
```

---

## Properties

```
name

length

prototype
```

---

Example

```javascript
function sum(a, b) {}
```

```
sum.name

↓

"sum"
```

```
sum.length

↓

2
```

---

## Named Function Expression (NFE)

```javascript
const sayHi = function greet() {
  console.log("Hello");
};
```

Outside

```
greet
```

doesn't exist.

Inside the function, `greet` refers to itself, which is useful for recursion or debugging.

---

# 6.7 The "new Function" Syntax

Functions can be created dynamically.

```javascript
const sum = new Function("a", "b", "return a+b");
```

Equivalent to

```javascript
function(a,b){

return a+b;

}
```

---

## Use Cases

```
Dynamic code generation

Templates

Expression evaluators
```

---

## Disadvantages

```
Slow

Hard to Debug

Security Risks if input is untrusted
```

Avoid it unless truly necessary.

---
