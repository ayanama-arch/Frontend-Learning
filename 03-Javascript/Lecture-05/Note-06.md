# 6.9 Decorators and Forwarding, call/apply

---

## Function Borrowing

Suppose

```javascript
function greet() {
  console.log(this.name);
}
```

Different objects can reuse it.

```javascript
greet.call(user);
```

---

## call()

```javascript
func.call(thisArg, arg1, arg2);
```

---

## apply()

Same idea

```javascript
func.apply(thisArg, argsArray);
```

Difference

```
call

↓

Arguments individually
```

```
apply

↓

Array of arguments
```

---

## bind()

Creates

```
New Function

↓

this fixed forever
```

```javascript
const hello = greet.bind(user);
```

---

## Decorators

A decorator

```
Original Function

↓

Extra Behavior

↓

Same Functionality
```

Example

```
Timing

Logging

Caching

Memoization
```

---

# 6.10 Function Binding

Problem

```javascript
const user = {
  name: "John",

  say() {
    console.log(this.name);
  },
};

setTimeout(user.say, 1000);
```

Output

```
undefined
```

because the method loses its original object.

---

Solution

```javascript
setTimeout(user.say.bind(user), 1000);
```

Now

```
John
```

---

Partial Application

```javascript
function multiply(a, b) {
  return a * b;
}

const double = multiply.bind(null, 2);
```

Calling

```javascript
double(5);
```

returns

```
10
```

---
