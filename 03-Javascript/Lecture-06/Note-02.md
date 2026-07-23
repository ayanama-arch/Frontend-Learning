# 7.2 Property Getters and Setters

---

# First Principle

Normally,

an object stores a value.

```
Property

↓

Value
```

Sometimes

you don't want to store a value.

Instead,

you want to **compute** it whenever someone reads it.

Or

you want validation whenever someone writes it.

That's exactly what **getters** and **setters** do.

---

# Getter

A getter behaves like a property

but actually runs a function.

Example

```javascript
const user = {
  firstName: "Ayan",

  lastName: "Khan",

  get fullName() {
    return this.firstName + " " + this.lastName;
  },
};

console.log(user.fullName);
```

Output

```
Ayan Khan
```

Notice

```
No parentheses
```

Although a function executes.

---

# Without Getter

Normally

```javascript
user.fullName();
```

With getter

```javascript
user.fullName;
```

Feels like a property.

---

# Setter

A setter runs whenever a value is assigned.

Example

```javascript
const user = {
  firstName: "",

  lastName: "",

  set fullName(value) {
    const parts = value.split(" ");

    this.firstName = parts[0];

    this.lastName = parts[1];
  },
};

user.fullName = "Ayan Khan";
```

Now

```javascript
console.log(user.firstName);
```

prints

```
Ayan
```

---

# Getter + Setter Together

```javascript
const user = {
  firstName: "Ayan",

  lastName: "Khan",

  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },

  set fullName(value) {
    const [first, last] = value.split(" ");

    this.firstName = first;

    this.lastName = last;
  },
};
```

---

# Validation Using Setter

```javascript
const user = {
  _age: 0,

  set age(value) {
    if (value < 0) {
      throw Error("Invalid Age");
    }

    this._age = value;
  },

  get age() {
    return this._age;
  },
};
```

Now

```javascript
user.age = -10;
```

throws an error.

---

# Why Use `_age`?

If the getter/setter used the same property name internally:

```javascript
set age(value){
    this.age = value;
}
```

it would call itself forever, causing:

```
Maximum Call Stack Size Exceeded
```

Using a different internal property (commonly `_age` or `#age` with private fields) avoids this recursion.

---

# Getter/Setter Using `defineProperty`

```javascript
const user = {
  firstName: "Ayan",

  lastName: "Khan",
};

Object.defineProperty(user, "fullName", {
  get() {
    return this.firstName + " " + this.lastName;
  },

  set(value) {
    const [f, l] = value.split(" ");

    this.firstName = f;

    this.lastName = l;
  },

  enumerable: true,

  configurable: true,
});
```

---

# Accessor Descriptor vs Data Descriptor

There are **two kinds of property descriptors**.

## Data Descriptor

Stores data.

```javascript
{
    value:100,
    writable:true,
    enumerable:true,
    configurable:true
}
```

---

## Accessor Descriptor

Stores functions instead.

```javascript
{
    get(){...},
    set(value){...},
    enumerable:true,
    configurable:true
}
```

A property **cannot** be both a data descriptor and an accessor descriptor at the same time.

---

# Real-World Uses

## Computed Properties

```javascript
get fullName() {
    return `${this.firstName} ${this.lastName}`;
}
```

---

## Validation

```javascript
set email(value) {
    if (!value.includes("@")) {
        throw new Error("Invalid email");
    }
    this._email = value;
}
```

---

## Read-Only Properties

```javascript
const circle = {
  radius: 10,
  get area() {
    return Math.PI * this.radius ** 2;
  },
};

console.log(circle.area);
```

Every time `radius` changes, `area` is automatically recalculated.

---

## Lazy Computation (Concept)

Sometimes a getter computes a value only when it's first requested, caches the result, and returns the cached value on future accesses. This pattern is useful for expensive calculations.

---

# Summary Table

| Topic                        | Core Idea                                                               |
| ---------------------------- | ----------------------------------------------------------------------- |
| Property Descriptor          | Hidden metadata that controls how a property behaves.                   |
| `writable`                   | Controls whether the property's value can change.                       |
| `enumerable`                 | Controls whether the property appears in loops and `Object.keys()`.     |
| `configurable`               | Controls whether a property can be deleted or reconfigured.             |
| `Object.defineProperty()`    | Creates or modifies a property with custom descriptors.                 |
| `Object.freeze()`            | Prevents adding, deleting, or modifying properties.                     |
| `Object.seal()`              | Prevents adding or deleting properties, but allows value changes.       |
| `Object.preventExtensions()` | Prevents adding new properties only.                                    |
| Getter                       | Computes a value when a property is read.                               |
| Setter                       | Runs logic or validation when a property is assigned.                   |
| Accessor Descriptor          | Defines properties using `get`/`set` instead of storing a direct value. |

### Key Takeaway

Every JavaScript object property is more than just a value—it is governed by **property descriptors** that define how it can be read, written, enumerated, and configured. Getters and setters build on this mechanism, allowing properties to behave like ordinary fields while executing custom logic behind the scenes. These features are fundamental to how many built-in JavaScript APIs and modern frameworks implement encapsulation and computed properties.
