# JavaScript Basic Operators & Maths — Quick Revision

Based on your uploaded notes.

---

## Operands & Operators

- **Operand** → Value an operator acts on.
- **Unary Operator** → One operand (`-x`, `+x`, `++x`)
- **Binary Operator** → Two operands (`a+b`, `a-b`)

---

## Arithmetic Operators

| Operator | Meaning                  |
| -------- | ------------------------ |
| `+`      | Addition / Concatenation |
| `-`      | Subtraction              |
| `*`      | Multiplication           |
| `/`      | Division                 |
| `%`      | Remainder (Modulus)      |
| `**`     | Exponentiation (Power)   |

Examples

```js
5 % 2; // 1
2 ** 3; // 8
4 ** 0.5; // 2 (Square root)
```

---

## String Concatenation (`+`)

If **either operand is a string**, `+` concatenates.

```js
"1" + 2; // "12"
2 + "1"; // "21"
2 + 2 + "1"; // "41"
"1" + 2 + 2; // "122"
```

> Only `+` works with strings like this.

---

## Unary Plus (`+value`)

Converts value to a number.

```js
+"10" + // 10
  true + // 1
  false + // 0
  ""; // 0
```

Equivalent to:

```js
Number(value);
```

---

## Operator Precedence

Higher precedence executes first.

```
()
Unary + -
**
* / %
+ -
=
```

- Parentheses `()` override precedence.
- Unary `+` has higher precedence than binary `+`.

---

## Assignment (`=`)

Assigns a value **and returns it**.

```js
let x = 2 + 3; // 5
```

###### Chaining

```js
a = b = c = 5;
```

Assigns **right → left**.

---

## Modify & Assign

Shortcut operators:

```js
+=
-=
*=
/=
%=
```

Example

```js
x += 5; // x = x + 5
```

---

## Increment / Decrement

```js
++
--
```

Increase/decrease by **1**.

---

#### Prefix vs Postfix

###### Prefix (`++x`)

- Increment first.
- Return **new** value.

```js
let x = 1;
++x; // 2
```

---

###### Postfix (`x++`)

- Return **old** value.
- Increment afterwards.

```js
let x = 1;
x++; // returns 1, x becomes 2
```

###### Rule ⭐

- Need updated value → `++x`
- Need old value → `x++`

---

## Bitwise Operators (Rare)

```
&
|
^
~
<<
>>
>>>
```

Used mainly in low-level programming (e.g., cryptography).

---

## Comma Operator (Rare)

Evaluates multiple expressions, returns **last** value.

```js
let x = (1 + 2, 3 + 4);

x; // 7
```

Very low precedence; use parentheses.

---

## Must Remember ⭐

- Unary → **1 operand**, Binary → **2 operands**.
- `%` = remainder, `**` = power.
- `+` concatenates if **any operand is a string**.
- Unary `+` converts to **number**.
- `=` is an **operator** and returns a value.
- Chained assignment works **right → left**.
- `+=`, `-=`, `*=`, `/=` are shorthand operators.
- `++x` → increment then return.
- `x++` → return then increment.
- Bitwise (`&`, `|`, `^`, `~`, `<<`, `>>`, `>>>`) and comma (`,`) operators are **rarely used**.

# JavaScript Comparisons — Quick Revision

Based on your notes.

---

## Comparison Operators

| Operator | Meaning                              |
| -------- | ------------------------------------ |
| `>`      | Greater than                         |
| `<`      | Less than                            |
| `>=`     | Greater than or equal                |
| `<=`     | Less than or equal                   |
| `==`     | Loose equality (type conversion)     |
| `===`    | Strict equality (no type conversion) |
| `!=`     | Loose inequality                     |
| `!==`    | Strict inequality                    |

All comparison operators return **`true`** or **`false`**.

---

## String Comparison

- Compared **character by character** (Unicode order).
- Lowercase letters have higher Unicode values than uppercase.

```js
"Z" > "A"; // true
"Glow" > "Glee"; // true
"Bee" > "Be"; // true
```

---

## Different Type Comparison

JavaScript converts values to **numbers**.

```js
"2" > 1; // true
"01" == 1; // true

true == 1; // true
false == 0; // true
```

---

## Loose vs Strict Equality

#### Loose (`==`)

- Performs **type conversion**.

```js
0 == false; // true
"" == false; // true
```

---

#### Strict (`===`)

- **No type conversion**.

```js
0 === false; // false
1 === "1"; // false
```

> ⭐ **Always prefer `===` and `!==`.**

---

## `null` vs `undefined`

###### Strict Equality

```js
null === undefined; // false
```

###### Loose Equality

```js
null == undefined; // true
```

They are equal **only to each other**.

---

## Strange Cases

```js
null > 0; // false
null == 0; // false
null >= 0; // true
```

Reason:

- Comparisons (`>`, `<`, `>=`, `<=`) convert `null` → `0`.
- `==` has special rules for `null` and `undefined`.

---

```js
undefined > 0; // false
undefined < 0; // false
undefined == 0; // false
```

Reason:

- `undefined` → `NaN`.
- `NaN` is never equal to or greater/less than anything.

---

## Best Practice ⭐

- ✅ Use `===` and `!==`.
- ✅ Check `null`/`undefined` separately.
- ❌ Avoid `<`, `>`, `<=`, `>=` with `null` or `undefined`.

---

## Must Remember ⭐

- Comparisons return **boolean**.
- Strings compare **character by character (Unicode)**.
- `==` → type conversion.
- `===` → no type conversion.
- `null == undefined` → `true`.
- `null === undefined` → `false`.
- `null >= 0` → `true`, but `null == 0` → `false`.
- `undefined` compared with numbers → always `false`.
- **Use `===` by default.**
