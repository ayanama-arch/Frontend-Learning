# Forms Deep Dive: The Essential Guide

## 1. Custom Form Validation

### Built-in Constraint Validation

```html
<input type="email" required />
<input type="number" min="1" max="100" />
<input type="text" pattern="[A-Za-z]{3,}" title="3+ letters only" />
```

**Attributes:**

- `required` - Must have value
- `min`/`max` - Numeric/date bounds
- `minlength`/`maxlength` - String length
- `pattern` - Regex validation

---

### Custom Validation Messages

```html
<form>
  <input type="email" id="email" required />
  <button type="submit">Submit</button>
</form>

<script>
  const email = document.getElementById("email");

  email.addEventListener("invalid", (e) => {
    if (email.validity.valueMissing) {
      email.setCustomValidity("Please enter your email");
    } else if (email.validity.typeMismatch) {
      email.setCustomValidity("Please enter a valid email");
    }
  });

  email.addEventListener("input", () => {
    email.setCustomValidity(""); // Clear on input
  });
</script>
```

---

### Validity State API

```javascript
const input = document.getElementById("myInput");

// Check validity
input.checkValidity(); // true/false
input.reportValidity(); // Shows validation message

// Validity properties
input.validity.valid; // Overall valid
input.validity.valueMissing; // required but empty
input.validity.typeMismatch; // Wrong type (email, url, etc.)
input.validity.patternMismatch; // Doesn't match pattern
input.validity.tooLong; // Exceeds maxlength
input.validity.tooShort; // Below minlength
input.validity.rangeUnderflow; // Below min
input.validity.rangeOverflow; // Above max
input.validity.stepMismatch; // Doesn't match step
input.validity.customError; // Custom validation failed

// Get error message
input.validationMessage;
```

---

### Custom Validation Example

```html
<form id="signupForm">
  <input type="password" id="password" required minlength="8" />
  <input type="password" id="confirm" required />
  <button type="submit">Sign Up</button>
</form>

<script>
  const form = document.getElementById("signupForm");
  const password = document.getElementById("password");
  const confirm = document.getElementById("confirm");

  confirm.addEventListener("input", () => {
    if (confirm.value !== password.value) {
      confirm.setCustomValidity("Passwords must match");
    } else {
      confirm.setCustomValidity("");
    }
  });

  form.addEventListener("submit", (e) => {
    if (!form.checkValidity()) {
      e.preventDefault();
      form.reportValidity();
    }
  });
</script>
```

---

### Disable Native Validation

```html
<form novalidate>
  <!-- Use your own validation -->
</form>
```

---

## 2. Form Events

### Key Events

```javascript
const form = document.getElementById("myForm");
const input = document.getElementById("myInput");

// Input changes
input.addEventListener("input", (e) => {
  console.log("Value:", e.target.value); // Fires on every keystroke
});

input.addEventListener("change", (e) => {
  console.log("Changed:", e.target.value); // Fires on blur (when done editing)
});

// Form submission
form.addEventListener("submit", (e) => {
  e.preventDefault(); // Stop default submission
  console.log("Submitting...");
});

// Form reset
form.addEventListener("reset", (e) => {
  console.log("Form reset");
});

// Invalid input
input.addEventListener("invalid", (e) => {
  console.log("Validation failed");
});

// Focus events
input.addEventListener("focus", () => console.log("Focused"));
input.addEventListener("blur", () => console.log("Lost focus"));
```

---

### Event Order

When submitting:

1. `invalid` (if validation fails)
2. `submit` (if validation passes)

When typing:

1. `input` (every keystroke)
2. `change` (on blur, if value changed)

---

### Practical Example: Live Validation

```html
<form id="userForm">
  <input type="text" id="username" required minlength="3" />
  <span id="usernameError"></span>
  <button type="submit">Submit</button>
</form>

<script>
  const username = document.getElementById("username");
  const error = document.getElementById("usernameError");

  username.addEventListener("input", () => {
    if (!username.validity.valid) {
      error.textContent = username.validationMessage;
      error.style.color = "red";
    } else {
      error.textContent = "✓";
      error.style.color = "green";
    }
  });
</script>
```

---

## 3. FormData API

### Basic Usage

```html
<form id="myForm">
  <input name="username" value="alice" />
  <input name="email" value="alice@example.com" />
  <input type="checkbox" name="subscribe" checked />
</form>

<script>
  const form = document.getElementById("myForm");
  const formData = new FormData(form);

  // Get values
  formData.get("username"); // 'alice'
  formData.get("email"); // 'alice@example.com'
  formData.get("subscribe"); // 'on'

  // Check if exists
  formData.has("username"); // true

  // Get all values (for multiple inputs with same name)
  formData.getAll("hobby"); // ['reading', 'coding']

  // Set/update values
  formData.set("username", "bob");
  formData.append("role", "admin"); // Add new field

  // Delete
  formData.delete("subscribe");

  // Iterate
  for (let [key, value] of formData) {
    console.log(`${key}: ${value}`);
  }
</script>
```

---

### Submit with Fetch

```javascript
form.addEventListener("submit", async (e) => {
  e.preventDefault();

  const formData = new FormData(form);

  try {
    const response = await fetch("/api/submit", {
      method: "POST",
      body: formData, // Automatically sets multipart/form-data
    });

    const result = await response.json();
    console.log("Success:", result);
  } catch (error) {
    console.error("Error:", error);
  }
});
```

---

### Send as JSON

```javascript
const formData = new FormData(form);
const data = Object.fromEntries(formData); // Convert to object

await fetch("/api/submit", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify(data),
});
```

---

### File Uploads

```html
<form id="uploadForm">
  <input type="file" name="avatar" accept="image/*" />
  <input type="file" name="documents" multiple />
  <button type="submit">Upload</button>
</form>

<script>
  uploadForm.addEventListener("submit", async (e) => {
    e.preventDefault();

    const formData = new FormData(uploadForm);

    // Check files
    const avatar = formData.get("avatar");
    console.log("Avatar:", avatar.name, avatar.size);

    // Get all files from multi-file input
    const docs = formData.getAll("documents");
    docs.forEach((file) => console.log(file.name));

    // Upload
    await fetch("/upload", {
      method: "POST",
      body: formData,
    });
  });
</script>
```

---

### Append Files Programmatically

```javascript
const formData = new FormData();

// Create a blob/file
const blob = new Blob(["Hello"], { type: "text/plain" });
const file = new File([blob], "hello.txt");

formData.append("file", file);
formData.append("username", "alice");
```

---

## 4. Form-Associated Custom Elements

### What They Are

Custom elements that behave like native form controls.

```javascript
class CustomInput extends HTMLElement {
  static formAssociated = true; // KEY: Makes it form-associated

  constructor() {
    super();
    this._internals = this.attachInternals(); // Access form internals
    this._value = "";
  }

  connectedCallback() {
    this.innerHTML = `<input type="text">`;
    this.input = this.querySelector("input");

    this.input.addEventListener("input", () => {
      this._value = this.input.value;
      this._internals.setFormValue(this._value); // Update form value
    });
  }

  // Form control API
  get value() {
    return this._value;
  }
  set value(v) {
    this._value = v;
    if (this.input) this.input.value = v;
    this._internals.setFormValue(v);
  }

  // Validation
  checkValidity() {
    if (this._value.length < 3) {
      this._internals.setValidity(
        { tooShort: true },
        "Must be at least 3 characters"
      );
      return false;
    }
    this._internals.setValidity({});
    return true;
  }

  // Called when form resets
  formResetCallback() {
    this.value = "";
  }

  // Called when form is disabled
  formDisabledCallback(disabled) {
    this.input.disabled = disabled;
  }
}

customElements.define("custom-input", CustomInput);
```

**Usage:**

```html
<form id="myForm">
  <custom-input name="username"></custom-input>
  <button type="submit">Submit</button>
</form>

<script>
  myForm.addEventListener("submit", (e) => {
    e.preventDefault();
    const formData = new FormData(myForm);
    console.log(formData.get("username")); // Works!
  });
</script>
```

---

### ElementInternals API

```javascript
const internals = this.attachInternals();

// Set form value
internals.setFormValue(value);
internals.setFormValue(value, state); // value + internal state

// Set validity
internals.setValidity(
  { valueMissing: true }, // Validity flags
  "This field is required", // Message
  anchorElement // Element to anchor error to (optional)
);

// Clear validity
internals.setValidity({});

// Get form
internals.form; // Parent <form> element

// Check states
internals.validity;
internals.validationMessage;
internals.willValidate;
```

---

### Practical Example: Star Rating

```javascript
class StarRating extends HTMLElement {
  static formAssociated = true;

  constructor() {
    super();
    this._internals = this.attachInternals();
    this._value = 0;
  }

  connectedCallback() {
    this.render();
  }

  render() {
    this.innerHTML = "";
    for (let i = 1; i <= 5; i++) {
      const star = document.createElement("span");
      star.textContent = i <= this._value ? "★" : "☆";
      star.style.cursor = "pointer";
      star.style.fontSize = "24px";
      star.onclick = () => this.rate(i);
      this.appendChild(star);
    }
  }

  rate(value) {
    this._value = value;
    this._internals.setFormValue(value);
    this.render();
    this.dispatchEvent(new Event("change", { bubbles: true }));
  }

  get value() {
    return this._value;
  }
  set value(v) {
    this.rate(v);
  }

  formResetCallback() {
    this.rate(0);
  }
}

customElements.define("star-rating", StarRating);
```

**Usage:**

```html
<form>
  <label>Rate this product:</label>
  <star-rating name="rating"></star-rating>
  <button type="submit">Submit</button>
</form>
```

---

## Quick Reference

### Validation

```javascript
input.setCustomValidity("Error message");
input.checkValidity(); // true/false
input.reportValidity(); // Show message
input.validity.valid; // Check state
```

### Events

```javascript
input.addEventListener("input", fn); // Every keystroke
input.addEventListener("change", fn); // On blur
form.addEventListener("submit", fn); // On submit
input.addEventListener("invalid", fn); // Validation failed
```

### FormData

```javascript
const fd = new FormData(form);
fd.get("name");
fd.set("name", "value");
fd.append("name", "value");
fd.delete("name");
```

### Form-Associated Elements

```javascript
static formAssociated = true;
this._internals = this.attachInternals();
this._internals.setFormValue(value);
this._internals.setValidity(flags, message);
```

---

## Key Takeaways

- **Custom validation:** Use `setCustomValidity()` + `validity` API
- **Events:** `input` (live), `change` (on blur), `submit` (form)
- **FormData:** Easy form serialization, works with fetch, handles files
- **Form-associated elements:** Make custom elements work like native inputs

HTML forms are powerful—master these APIs to build robust, accessible forms without libraries.
