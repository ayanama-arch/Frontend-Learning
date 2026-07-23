# 5.12 JSON Methods, `toJSON`

## What is JSON?

**JSON (JavaScript Object Notation)** is a lightweight text format for representing structured data. Although inspired by JavaScript object syntax, it is language-independent and widely used for communication between clients and servers.

Example JSON:

```json
{
  "name": "Ayan",
  "age": 23,
  "isStudent": false
}
```

### Rules

- Keys must be enclosed in **double quotes**.
- Values can be:
  - String
  - Number
  - Boolean
  - `null`
  - Object
  - Array

- Functions, `undefined`, and `Symbol` values are **not valid JSON**.

---

## `JSON.stringify()`

Converts a JavaScript value into a JSON string.

```javascript
const user = {
  name: "Ayan",
  age: 23,
};

const json = JSON.stringify(user);

console.log(json);
// {"name":"Ayan","age":23}
```

### Common Use Cases

- Sending data in HTTP requests
- Saving objects in `localStorage`
- Logging or exporting structured data

---

## `JSON.parse()`

Converts a JSON string back into a JavaScript value.

```javascript
const json = '{"name":"Ayan","age":23}';

const obj = JSON.parse(json);

console.log(obj.name);
// Ayan
```

---

## Pretty Printing

```javascript
const user = { name: "Ayan", age: 23 };

console.log(JSON.stringify(user, null, 2));
```

Output:

```json
{
  "name": "Ayan",
  "age": 23
}
```

The third argument specifies the indentation level.

---

## Replacer Function

You can customize serialization.

```javascript
const user = {
  name: "Ayan",
  password: "secret123",
};

const json = JSON.stringify(user, (key, value) => {
  if (key === "password") return undefined;
  return value;
});

console.log(json);
// {"name":"Ayan"}
```

---

## Reviver Function

Transform values while parsing.

```javascript
const json = '{"created":"2026-07-24T10:00:00.000Z"}';

const obj = JSON.parse(json, (key, value) => {
  if (key === "created") {
    return new Date(value);
  }
  return value;
});

console.log(obj.created instanceof Date);
// true
```

---

## `toJSON()`

If an object defines a `toJSON()` method, `JSON.stringify()` calls it automatically.

```javascript
const user = {
  name: "Ayan",
  age: 23,
  toJSON() {
    return {
      name: this.name,
    };
  },
};

console.log(JSON.stringify(user));
// {"name":"Ayan"}
```

This is useful when you want to control exactly how an object is serialized.

---

# Summary Table

| Topic                        | Core Idea                                                                                       |
| ---------------------------- | ----------------------------------------------------------------------------------------------- |
| Methods of primitives        | Primitives temporarily gain methods through wrapper objects                                     |
| Numbers                      | One `Number` type (IEEE-754), plus `BigInt` for huge integers                                   |
| Strings                      | Immutable UTF-16 sequences with rich manipulation methods                                       |
| Arrays                       | Dynamic ordered collections supporting many functional operations                               |
| Array methods                | `map`, `filter`, `reduce`, `find`, `sort`, and more for data processing                         |
| Iterables                    | Objects implementing `Symbol.iterator`, usable with `for...of`                                  |
| Map & Set                    | `Map` stores arbitrary key-value pairs; `Set` stores unique values                              |
| WeakMap & WeakSet            | Weakly referenced collections that aid garbage collection                                       |
| `Object.keys/values/entries` | Convert object properties into iterable arrays                                                  |
| Destructuring                | Concise extraction of values from arrays and objects                                            |
| Date & Time                  | Work with timestamps, formatting, parsing, and calculations                                     |
| JSON                         | Serialize (`stringify`) and deserialize (`parse`) structured data for storage and communication |
