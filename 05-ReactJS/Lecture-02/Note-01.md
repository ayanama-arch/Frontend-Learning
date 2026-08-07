# React Event Handling (Revision Notes)

## 1. Adding Event Handlers

```jsx
function handleClick() {
  alert("Clicked!");
}

<button onClick={handleClick}>Click</button>;
```

- Define handler inside component.
- Pass function reference to event prop.
- Naming convention: `handle + EventName`
  - `handleClick`
  - `handleSubmit`
  - `handleChange`

---

## 2. Ways to Write Event Handlers

Separate function

```jsx
<button onClick={handleClick} />
```

Inline function

```jsx
<button
  onClick={function () {
    alert("Clicked");
  }}
/>
```

Arrow function

```jsx
<button onClick={() => alert("Clicked")} />
```

✅ All are equivalent.

---

## 3. Don't Call the Function

✅ Correct

```jsx
<button onClick={handleClick}>
```

❌ Wrong

```jsx
<button onClick={handleClick()}>
```

**Remember:**

- `handleClick` → pass function
- `handleClick()` → execute immediately

---

## 4. Inline Handler Mistake

❌ Wrong

```jsx
<button onClick={alert("Hello")}>
```

Runs during rendering.

✅ Correct

```jsx
<button onClick={() => alert("Hello")}>
```

Creates a function to run later.

---

# Props in Event Handlers

Event handlers can access component props.

```jsx
function Button({ message }) {
  return <button onClick={() => alert(message)}>Click</button>;
}
```

---

# Passing Event Handlers as Props

Parent decides what happens.

```jsx
<Button onClick={handleClick} />
```

Child

```jsx
function Button({ onClick }) {
  return <button onClick={onClick}>Click</button>;
}
```

This keeps components reusable.

---

# Naming Event Handler Props

Built-in HTML

```jsx
<button onClick={...}>
```

Custom components

```jsx
<Button onSmash={...}>
<Button onPlayMovie={...}>
<Button onUploadImage={...}>
```

Convention:

```
on + Action
```

Examples

- onSave
- onDelete
- onLogin
- onSubmit
- onPlayMovie

---

# Use Semantic HTML

✅ Good

```jsx
<button onClick={...}>
```

❌ Avoid

```jsx
<div onClick={...}>
```

Reason:

- Better accessibility
- Keyboard support
- Browser behavior

---

# Event Propagation (Bubbling)

Events move **from child → parent**.

```jsx
<div onClick={...}>
    <button onClick={...}>
```

Click button:

```
Button onClick
      ↓
Parent onClick
```

Both run.

---

# Stop Propagation

Prevent event from reaching parent.

```jsx
<button onClick={(e) => {
    e.stopPropagation();
    onClick();
}}>
```

Result:

```
Button runs ✅
Parent does NOT run ❌
```

---

# Event Object (`e`)

Every handler receives an event object.

```jsx
function handleClick(e) {
  console.log(e);
}
```

Useful methods:

```jsx
e.stopPropagation();
e.preventDefault();
```

---

# Capture Phase

Normally:

```
Capture
   ↓
Target
   ↓
Bubble
```

Use

```jsx
<div onClickCapture={...}>
```

Execution order

```
onClickCapture
      ↓
Clicked element's onClick
      ↓
Parent onClick
```

Useful for:

- Analytics
- Logging
- Routers

Rarely used.

---

# Alternative to Propagation

Instead of relying on bubbling:

```jsx
function Button({ onClick }) {
    return (
        <button onClick={(e)=>{
            e.stopPropagation();

            // child logic

            onClick();
        }}>
```

Flow

```
Child logic
      ↓
Parent callback
```

More explicit and easier to trace.

---

# Prevent Default Behavior

Some browser events have default actions.

Example:

```
<form>
```

Default:

- Page reloads on submit.

Prevent it

```jsx
<form onSubmit={(e)=>{
    e.preventDefault();
}}>
```

---

# stopPropagation vs preventDefault

| Method                | Purpose                        |
| --------------------- | ------------------------------ |
| `e.stopPropagation()` | Stops event bubbling to parent |
| `e.preventDefault()`  | Stops browser's default action |

Examples:

```
stopPropagation()
```

Stops

```
Button
 ↓
Parent
```

---

```
preventDefault()
```

Stops

```
Form Submit
↓
Page Reload
```

---

# Side Effects

Event handlers are the **correct place** for side effects.

Examples:

- API calls
- Updating state
- Showing alerts
- Changing input values
- Modifying lists

Rendering should stay pure; event handlers can perform side effects.

---

# Quick Revision Checklist ✅

- Pass function, don't call it.
- Event handlers usually start with `handle`.
- Handlers can access props.
- Parent can pass handlers to children.
- Custom handler props usually start with `on`.
- Use `<button>` instead of clickable `<div>`.
- Events bubble from child → parent.
- `e.stopPropagation()` stops bubbling.
- `onClickCapture` runs during capture phase (before target/bubble).
- `e.preventDefault()` stops browser default behavior.
- Event handlers are the right place for side effects.
