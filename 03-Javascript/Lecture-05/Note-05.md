# 6.8 Scheduling: setTimeout and setInterval

JavaScript can schedule future work.

---

## setTimeout

Runs once.

```javascript
setTimeout(() => {
  console.log("Hello");
}, 2000);
```

```
Wait

↓

2 seconds

↓

Run
```

---

## Cancel

```javascript
const id = setTimeout(...);

clearTimeout(id);
```

---

## setInterval

Runs repeatedly.

```javascript
setInterval(() => {
  console.log("Tick");
}, 1000);
```

```
1 sec

↓

Tick

↓

1 sec

↓

Tick
```

---

## Stop Interval

```javascript
clearInterval(id);
```

---

## Nested Timeout

Instead of

```javascript
setInterval();
```

Many developers use

```javascript
function repeat() {
  setTimeout(() => {
    repeat();
  }, 1000);
}
```

It provides better control because the next timer is scheduled after the current work finishes.

---
