# Microdata & Structured Data

---

# The Problem

Imagine a webpage saying

```html
Apple
```

To a human, this could mean

- Apple Inc.
- Apple fruit
- Apple Records

A computer has no idea.

Now imagine

```html
Apple Inc. CEO: Tim Cook Founded: 1976
```

Humans understand it instantly.

Computers still struggle.

Structured data solves this.

---

# What is Structured Data?

Structured Data is additional information embedded inside HTML that describes the meaning of your content.

Instead of saying

> Here is some text.

You tell machines

> This is a Product.

> This is a Person.

> This is a Recipe.

> This is a Movie.

> This is an Organization.

Think of it as metadata for machines.

---

# Without Structured Data

```html
<h1>iPhone 16 Pro</h1>

<p>Price ₹1,19,999</p>
```

Human

> Nice.

Google

> Maybe product...
>
> Maybe article...
>
> Maybe blog...
>
> Maybe advertisement...

---

# With Structured Data

```text
Product
 ├── Name
 ├── Brand
 ├── Price
 ├── Currency
 ├── Availability
 └── Rating
```

Now Google knows exactly what it is.

---

# Why Does It Matter?

Search engines can show

- Ratings ⭐⭐⭐⭐⭐
- Price
- Recipe time
- Calories
- FAQ
- Breadcrumbs
- Event dates
- Job salaries

These are called

> Rich Results (formerly Rich Snippets)

Example

Instead of

```
Chocolate Cake Recipe
```

Google can display

```
⭐⭐⭐⭐⭐ 4.9
30 min
450 calories
```

---

# How Structured Data Works

Three parts

```
Content

↓

Schema Vocabulary

↓

Search Engine understands
```

---

# What is Schema?

Schema is a standardized vocabulary.

Instead of inventing your own words

```
productName
```

Everyone agrees to use

```
name
```

Instead of

```
cost
```

Everyone uses

```
price
```

Instead of

```
seller
```

Everyone uses

```
offers
```

This common language is maintained by **Schema.org**.

---

# Schema.org Vocabulary

Schema.org contains thousands of predefined types.

Examples

```
Person

Organization

Product

Book

Movie

Recipe

Course

Restaurant

Hotel

Review

FAQPage

Article

NewsArticle

VideoObject

JobPosting

Event

LocalBusiness

MedicalEntity

SoftwareApplication

Vehicle
```

Each has properties.

Example

```
Person

├── name
├── age
├── birthDate
├── gender
├── nationality
├── address
└── jobTitle
```

---

# Example Product Schema

```text
Product

├── name
├── image
├── description
├── sku
├── brand
├── price
├── currency
├── rating
├── reviews
└── availability
```

---

# Ways to Add Structured Data

There are four major methods.

```
Structured Data

├── JSON-LD ⭐ Recommended
├── Microdata
├── RDFa
└── Microformats
```

Let's study each.

---

# 1. JSON-LD (Recommended)

JSON-LD stands for

**JavaScript Object Notation for Linked Data**

It is simply JSON placed inside

```html
<script type="application/ld+json">
```

This does NOT execute as JavaScript.

It only contains machine-readable data.

---

## Example

```html
<script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Person",
    "name": "John Doe",
    "jobTitle": "Software Engineer",
    "email": "john@example.com"
  }
</script>
```

Nothing appears on the page.

Humans never see it.

Search engines do.

---

## Product Example

```html
<script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Product",
    "name": "Wireless Mouse",
    "brand": {
      "@type": "Brand",
      "name": "Logitech"
    },
    "offers": {
      "@type": "Offer",
      "price": "1299",
      "priceCurrency": "INR",
      "availability": "https://schema.org/InStock"
    }
  }
</script>
```

---

## Why Google Recommends JSON-LD

Because HTML stays clean.

Bad

```html
<div itemscope itemtype="..."></div>
```

Good

```html
<script type="application/ld+json">

  ...
</script>
```

Presentation and metadata remain separate.

---

# Anatomy of JSON-LD

```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "John"
}
```

---

## @context

Tells which vocabulary is used.

```json
"@context":"https://schema.org"
```

---

## @type

Defines object type.

```json
"@type":"Book"
```

or

```json
"@type":"Recipe"
```

or

```json
"@type":"Movie"
```

---

## Properties

Everything else.

```
name

author

price

rating

review

image
```

---

# Nested Objects

```json
{
  "@type": "Book",

  "author": {
    "@type": "Person",
    "name": "J.K. Rowling"
  }
}
```

Objects can contain other objects.

---

# Multiple Objects

```json
[
  {
    "@type": "Person",
    "name": "Alice"
  },

  {
    "@type": "Organization",
    "name": "Google"
  }
]
```

---

# 2. Microdata

Microdata embeds metadata directly into HTML elements.

Instead of separate JSON,

you decorate existing HTML.

---

## Example

```html
<div itemscope itemtype="https://schema.org/Person">
  <h1 itemprop="name">John Doe</h1>

  <p itemprop="jobTitle">Software Engineer</p>
</div>
```

---

## New Attributes

### itemscope

Creates an item.

```html
<div itemscope></div>
```

---

### itemtype

Specifies type.

```html
itemtype="https://schema.org/Product"
```

---

### itemprop

Defines property.

```html
itemprop="price"
```

---

## Product Example

```html
<div itemscope itemtype="https://schema.org/Product">
  <h2 itemprop="name">Wireless Mouse</h2>

  <p itemprop="description">Ergonomic Bluetooth Mouse</p>

  <span itemprop="price"> 1299 </span>
</div>
```

---

# Advantages

- HTML and metadata together
- Easy for small pages

---

# Disadvantages

HTML becomes cluttered.

```html
<div itemscope
itemtype="..."
itemprop="..."
```

Large pages become hard to maintain.

---

# 3. RDFa

RDFa stands for:

**Resource Description Framework in Attributes**

It is an extension of HTML that embeds semantic information using a richer set of attributes than Microdata.

Common attributes:

- `typeof`
- `property`
- `resource`
- `vocab`
- `about`

Example:

```html
<div vocab="https://schema.org/" typeof="Person">
  <span property="name">John Doe</span>
  <span property="jobTitle">Software Engineer</span>
</div>
```

RDFa is very flexible and can express relationships between resources beyond what Microdata easily supports. It is common in semantic web and linked-data applications but less common for everyday SEO.

---

# 4. Microformats

Microformats predate Schema.org.

Instead of using Schema.org attributes, they use predefined CSS class names.

Example (`h-card` for a person):

```html
<div class="h-card">
  <span class="p-name">John Doe</span>
  <a class="u-email" href="mailto:john@example.com"> john@example.com </a>
</div>
```

Examples of common microformats:

- `h-card` — Person or organization
- `h-event` — Event
- `h-entry` — Blog post
- `h-review` — Review

Microformats are lightweight and still supported by some tools, but they are much less common than JSON-LD.

---

# Comparison

| Feature               | JSON-LD    | Microdata | RDFa      | Microformats |
| --------------------- | ---------- | --------- | --------- | ------------ |
| Separate from HTML    | ✅         | ❌        | ❌        | ❌           |
| Uses Schema.org       | ✅         | ✅        | ✅        | ❌           |
| HTML stays clean      | ✅         | ❌        | ❌        | ✅           |
| Recommended by Google | ✅         | Supported | Supported | Limited      |
| Best for SEO          | ⭐⭐⭐⭐⭐ | ⭐⭐⭐    | ⭐⭐⭐    | ⭐           |

---

# Which One Should You Use?

For modern websites:

- **JSON-LD** → Preferred and recommended by Google for almost all SEO use cases.
- **Microdata** → Mostly found on older sites or CMS templates.
- **RDFa** → Useful for semantic web and linked-data applications requiring complex relationships.
- **Microformats** → Mainly for legacy compatibility and niche use cases.

---

# Real-World Examples

## E-commerce

```text
Product
├── Name
├── Price
├── Currency
├── Brand
├── Rating
├── Availability
└── Reviews
```

Enables product rich results.

---

## Recipe Website

```text
Recipe
├── Ingredients
├── Cooking Time
├── Calories
├── Nutrition
├── Rating
└── Author
```

Can display cooking time, ratings, and nutritional information in search.

---

## News Website

```text
Article
├── Headline
├── Date Published
├── Author
├── Image
└── Publisher
```

Helps search engines understand news content and eligibility for certain search features.

---

## Course Website

```text
Course
├── Name
├── Provider
├── Description
├── Duration
└── Instructor
```

---

# Best Practices

- Use **JSON-LD** whenever possible.
- Keep structured data consistent with what users actually see on the page.
- Use the correct Schema.org type and properties.
- Validate your markup with Google's Rich Results Test or the Schema Markup Validator before deploying.
- Don't mark up content that doesn't exist on the page or use misleading data.

---

# Interview Questions

1. What is structured data, and why is it important?
2. What problem does Schema.org solve?
3. What is the difference between Microdata, RDFa, JSON-LD, and Microformats?
4. Why does Google recommend JSON-LD?
5. What are `@context` and `@type` in JSON-LD?
6. Explain `itemscope`, `itemtype`, and `itemprop` in Microdata.
7. What are rich results, and how does structured data enable them?
8. Can structured data improve SEO rankings directly? (No. It does not directly boost rankings, but it can improve visibility and click-through rates through rich results.)

## Key Takeaway

Think of structured data as **a language for machines**. Your HTML tells browsers **how to display** content, while structured data tells search engines, AI systems, and other software **what that content actually means**. Today, **JSON-LD + Schema.org** is the industry-standard approach for adding that semantic meaning to web pages.
