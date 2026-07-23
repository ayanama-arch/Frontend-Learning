# Web Components: The Essential Guide

## The Problem

HTML gives you `<div>`, `<span>`, `<button>`. But what if you need `<date-picker>`, `<video-player>`, or `<user-card>`?

**Traditional solutions:**

- jQuery plugins → Global namespace pollution
- Framework components → Locked to React/Vue/Angular
- Copy-paste HTML → No encapsulation, CSS conflicts

**The solution:** Web Components = native, reusable, framework-agnostic components.

---

## Three Core Technologies

Web Components aren't a single thing—they're three browser APIs working together:

1. **Custom Elements** → Define your own HTML tags
2. **Shadow DOM** → Encapsulate styles and markup
3. **HTML Templates** → Reusable markup chunks

**(+ HTML Imports** → Deprecated, but understanding why matters)

---

## 1. Custom Elements

### What They Do

Let you create your own HTML tags with custom behavior.

```html
<user-card name="Alice" role="Developer"></user-card>
```

Instead of:

```html
<div class="user-card">
  <h3 class="user-card__name">Alice</h3>
  <p class="user-card__role">Developer</p>
</div>
```

---

### Defining a Custom Element

```javascript
class UserCard extends HTMLElement {
  constructor() {
    super();
    // Element created (not yet in DOM)
  }

  connectedCallback() {
    // Element added to DOM - render here
    const name = this.getAttribute("name");
    const role = this.getAttribute("role");

    this.innerHTML = `
      <div class="card">
        <h3>${name}</h3>
        <p>${role}</p>
      </div>
    `;
  }

  disconnectedCallback() {
    // Element removed from DOM - cleanup here
  }

  attributeChangedCallback(name, oldValue, newValue) {
    // Attribute changed - update here
  }

  static get observedAttributes() {
    // Which attributes trigger attributeChangedCallback
    return ["name", "role"];
  }
}

// Register the element
customElements.define("user-card", UserCard);
```

**Now you can use it:**

```html
<user-card name="Bob" role="Designer"></user-card>
```

---

### Lifecycle Callbacks

| Callback                     | When It Fires         | Use Case                           |
| ---------------------------- | --------------------- | ---------------------------------- |
| `constructor()`              | Element created       | Initialize state (don't touch DOM) |
| `connectedCallback()`        | Added to DOM          | Render, fetch data, add listeners  |
| `disconnectedCallback()`     | Removed from DOM      | Cleanup, remove listeners          |
| `attributeChangedCallback()` | Attribute changes     | Re-render on prop changes          |
| `adoptedCallback()`          | Moved to new document | Rare - iframe scenarios            |

---

### Naming Rules

**Required:** Custom element names must contain a hyphen (`-`)

```javascript
// ✅ Valid
customElements.define("user-card", UserCard);
customElements.define("my-button", MyButton);

// ❌ Invalid
customElements.define("usercard", UserCard); // No hyphen
customElements.define("button", MyButton); // Reserved name
```

**Why?** Prevents conflicts with current and future HTML elements.

---

## 2. Shadow DOM

### The Problem It Solves

Normal DOM has no style encapsulation:

```html
<style>
  .card {
    background: red;
  }
</style>

<div class="card">My card</div>
<user-card></user-card>
<!-- Also affected by .card styles! -->
```

CSS leaks everywhere. Shadow DOM fixes this.

---

### What Shadow DOM Does

Creates an **isolated DOM tree** attached to an element.

- Styles inside can't leak out
- Styles outside can't leak in
- Markup is hidden from the main document

**Think of it as an invisible boundary.**

---

### Creating Shadow DOM

```javascript
class UserCard extends HTMLElement {
  constructor() {
    super();

    // Attach shadow root
    this.attachShadow({ mode: "open" });

    this.shadowRoot.innerHTML = `
      <style>
        /* These styles ONLY apply inside this component */
        .card {
          background: #f0f0f0;
          padding: 20px;
          border-radius: 8px;
        }
        
        h3 {
          margin: 0;
          color: #333;
        }
      </style>
      
      <div class="card">
        <h3>${this.getAttribute("name")}</h3>
        <p>${this.getAttribute("role")}</p>
      </div>
    `;
  }
}

customElements.define("user-card", UserCard);
```

**Key points:**

- `{ mode: 'open' }` → JavaScript can access `element.shadowRoot`
- `{ mode: 'closed' }` → No external access (rare, harder to debug)

---

### Shadow DOM in Action

```html
<style>
  /* Global styles */
  .card {
    background: red !important;
  }
  h3 {
    color: blue !important;
  }
</style>

<div class="card">
  <h3>Regular card</h3>
  <p>Affected by global styles</p>
</div>

<user-card name="Alice" role="Developer"></user-card>
<!-- NOT affected - has its own encapsulated styles -->
```

The `<user-card>` is immune to global CSS.

---

### Shadow DOM Slots

**Problem:** How do users pass content into your component?

**Solution:** Slots = placeholders for user content.

```javascript
class UserCard extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: "open" });

    this.shadowRoot.innerHTML = `
      <style>
        .card { padding: 20px; background: #f0f0f0; }
      </style>
      
      <div class="card">
        <slot name="header"></slot>
        <slot></slot> <!-- Default slot -->
        <slot name="footer"></slot>
      </div>
    `;
  }
}

customElements.define("user-card", UserCard);
```

**Usage:**

```html
<user-card>
  <h2 slot="header">Alice Johnson</h2>
  <p>Senior Developer with 5 years experience.</p>
  <button slot="footer">Contact</button>
</user-card>
```

**Result:**

- Content with `slot="header"` goes into `<slot name="header">`
- Content without slot attribute goes into default `<slot>`
- Styles from outside still apply to slotted content

---

## 3. HTML Templates

### The Problem

Creating HTML in JavaScript strings is messy:-

```javascript
this.innerHTML = `
  <div class="card">
    <h3>${name}</h3>
    <p>${role}</p>
  </div>
`;
```

Issues:

- No syntax highlighting
- No error checking
- String concatenation hell
- Evaluated immediately

---

### What `<template>` Does

Holds inert HTML that can be cloned and activated later.

```html
<template id="user-card-template">
  <style>
    .card {
      background: #f0f0f0;
      padding: 20px;
    }
  </style>

  <div class="card">
    <h3 class="name"></h3>
    <p class="role"></p>
  </div>
</template>
```

**Key trait:** Content inside `<template>` is:

- Parsed but not rendered
- Images don't load
- Scripts don't execute
- Zero performance cost until cloned

---

### Using Templates

```javascript
class UserCard extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: "open" });

    // Get the template
    const template = document.getElementById("user-card-template");

    // Clone it
    const clone = template.content.cloneNode(true);

    // Populate it
    clone.querySelector(".name").textContent = this.getAttribute("name");
    clone.querySelector(".role").textContent = this.getAttribute("role");

    // Add to shadow DOM
    this.shadowRoot.appendChild(clone);
  }
}

customElements.define("user-card", UserCard);
```

**Benefits:**

- Cleaner than string concatenation
- Parsed once, cloned many times
- Better performance for repeated components

---

### Template vs String Literals

| Approach              | Pros                           | Cons                             |
| --------------------- | ------------------------------ | -------------------------------- |
| **Template literals** | Simple, inline, dynamic        | No reuse, no syntax highlighting |
| **`<template>` tag**  | Reusable, parsed once, cleaner | Requires HTML in document        |

**Rule of thumb:** Use `<template>` for complex, reused components. Use template literals for simple, one-off components.

---

## 4. HTML Imports (Deprecated)

### What They Were

A way to import HTML documents into other HTML documents:

```html
<link rel="import" href="user-card.html" />
```

**Goal:** Bundle component HTML, CSS, and JS in one file.

---

### Why They Failed

- Only implemented in Chrome
- ES Modules solved the same problem better
- Officially deprecated in 2019

**The replacement:** ES Modules

```javascript
// user-card.js
class UserCard extends HTMLElement {
  /* ... */
}
customElements.define("user-card", UserCard);
export default UserCard;
```

```html
<!-- In your HTML -->
<script type="module">
  import UserCard from "./user-card.js";
</script>
```

**Lesson:** HTML Imports showed the need for component packaging, but JavaScript modules won.

---

## Putting It All Together

### Complete Example: Toggle Button

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Web Component Demo</title>
  </head>
  <body>
    <toggle-button></toggle-button>
    <toggle-button active></toggle-button>

    <template id="toggle-template">
      <style>
        button {
          padding: 10px 20px;
          border: 2px solid #333;
          background: white;
          cursor: pointer;
          font-size: 16px;
          border-radius: 4px;
          transition: all 0.2s;
        }

        button.active {
          background: #333;
          color: white;
        }
      </style>

      <button>
        <slot>Toggle</slot>
      </button>
    </template>

    <script>
      class ToggleButton extends HTMLElement {
        constructor() {
          super();
          this.attachShadow({ mode: "open" });

          // Clone template
          const template = document.getElementById("toggle-template");
          this.shadowRoot.appendChild(template.content.cloneNode(true));

          // Get button reference
          this.button = this.shadowRoot.querySelector("button");

          // Add event listener
          this.button.addEventListener("click", () => this.toggle());
        }

        connectedCallback() {
          // Set initial state
          if (this.hasAttribute("active")) {
            this.button.classList.add("active");
          }
        }

        toggle() {
          this.button.classList.toggle("active");

          // Dispatch custom event
          this.dispatchEvent(
            new CustomEvent("toggle", {
              detail: { active: this.button.classList.contains("active") },
            })
          );
        }

        static get observedAttributes() {
          return ["active"];
        }

        attributeChangedCallback(name, oldValue, newValue) {
          if (name === "active") {
            if (newValue !== null) {
              this.button.classList.add("active");
            } else {
              this.button.classList.remove("active");
            }
          }
        }
      }

      customElements.define("toggle-button", ToggleButton);

      // Usage
      document
        .querySelector("toggle-button")
        .addEventListener("toggle", (e) => {
          console.log("Button toggled:", e.detail.active);
        });
    </script>
  </body>
</html>
```

This component has:

- ✅ Custom element (`<toggle-button>`)
- ✅ Shadow DOM (style encapsulation)
- ✅ HTML template (reusable markup)
- ✅ Slots (customizable text)
- ✅ Attributes (declarative API)
- ✅ Events (communication)

---

## Web Components vs Frameworks

| Feature               | Web Components         | React/Vue/Angular        |
| --------------------- | ---------------------- | ------------------------ |
| **Browser support**   | Native, no build step  | Requires build tools     |
| **Framework lock-in** | None                   | Tied to framework        |
| **Learning curve**    | Steeper initially      | Easier with docs         |
| **Ecosystem**         | Smaller                | Massive                  |
| **Performance**       | Fast (native)          | Fast (with optimization) |
| **Use case**          | Reusable UI primitives | Full applications        |

**Best practice:** Use Web Components for design system components. Use frameworks for application logic.

---

## Common Patterns

### Reactive Properties

```javascript
class Counter extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: "open" });
    this._count = 0;
  }

  get count() {
    return this._count;
  }

  set count(val) {
    this._count = val;
    this.render();
  }

  connectedCallback() {
    this.render();
  }

  render() {
    this.shadowRoot.innerHTML = `
      <style>
        button { font-size: 20px; padding: 10px; }
        span { margin: 0 10px; font-size: 20px; }
      </style>
      <button id="dec">-</button>
      <span>${this.count}</span>
      <button id="inc">+</button>
    `;

    this.shadowRoot.getElementById("inc").onclick = () => this.count++;
    this.shadowRoot.getElementById("dec").onclick = () => this.count--;
  }
}

customElements.define("count-er", Counter);
```

---

### External Styles (CSS Custom Properties)

Shadow DOM blocks external styles, but CSS custom properties penetrate:

```html
<style>
  /* Global styles */
  :root {
    --primary-color: #007bff;
    --border-radius: 8px;
  }
</style>

<script>
  class ThemedCard extends HTMLElement {
    constructor() {
      super();
      this.attachShadow({ mode: "open" });

      this.shadowRoot.innerHTML = `
        <style>
          .card {
            background: var(--primary-color, #ccc);
            border-radius: var(--border-radius, 4px);
            padding: 20px;
          }
        </style>
        <div class="card">
          <slot></slot>
        </div>
      `;
    }
  }

  customElements.define("themed-card", ThemedCard);
</script>
```

Users can theme your component without breaking encapsulation.

---

## Browser Support

| Technology      | Support             |
| --------------- | ------------------- |
| Custom Elements | All modern browsers |
| Shadow DOM      | All modern browsers |
| HTML Templates  | All modern browsers |
| HTML Imports    | ❌ Deprecated       |

**IE11?** Use polyfills or skip Web Components.

---

## When to Use Web Components

**✅ Good for:**

- Design system components (`<button>`, `<card>`, `<dropdown>`)
- Reusable widgets across multiple projects/frameworks
- Third-party embeddable components
- Long-term maintainability (no framework churn)

**❌ Not ideal for:**

- Full applications (frameworks are better)
- Server-side rendering (limited support)
- Complex state management (use with a state library)
- Rapid prototyping (frameworks are faster)

---

## Key Takeaway

**Web Components = native, reusable, framework-agnostic components**

Three APIs working together:

1. **Custom Elements** → Define tags
2. **Shadow DOM** → Encapsulate styles
3. **Templates** → Reusable markup

Write once, use everywhere—in React, Vue, vanilla JS, or any future framework.
