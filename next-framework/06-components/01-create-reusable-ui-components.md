**Phase 5 — Components**

# Step 1: Create Reusable UI Components

According to our roadmap, you've completed:

* ✅ Phase 1 — Foundation
* ✅ Phase 2 — React Fundamentals
* ✅ Phase 3 — App Router
* ✅ Phase 4 — Styling

---

## Learning Goal

By the end of this lesson, you should be able to answer:

* What is a reusable component?
* Why do we create components?
* When should we create a component?
* What are the benefits of reusable components?
* How do we use the same component multiple times?

That's it.

---

## What is a Component?

Think about a real house.

A house is built from many smaller parts.

```
House
│
├── Door
├── Window
├── Roof
├── Kitchen
└── Bedroom
```

Each part has its own responsibility.

You don't build the entire house as one giant object.

---

Next.js (and React) works exactly the same way.

Instead of writing one huge page, we split it into small reusable pieces.

Example:

```
Home Page
│
├── Navbar
├── Hero Section
├── Features
├── Testimonials
├── Footer
```

Each piece is called a **Component**.

---

## Why Do We Need Components?

Imagine you have this HTML:

```html
<header>
  <h1>My Website</h1>

  <nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
    <a href="/contact">Contact</a>
  </nav>
</header>
```

Now imagine you have:

* Home page
* About page
* Contact page
* Blog page
* Dashboard

If you copy this HTML into every page:

```
Home
↓

Header

About
↓

Header

Contact
↓

Header

Blog
↓

Header
```

You now have the same code repeated many times.

#

Suppose you want to change:

```
About
```

to

```
About Us
```

You would have to update every page.

This is called **code duplication**.

---

## The Better Solution

Instead, create one component.

```
Navbar
```

Then use it everywhere.

```
Home
│
└── Navbar

About
│
└── Navbar

Contact
│
└── Navbar

Blog
│
└── Navbar
```

Now, if you update the Navbar once, every page automatically shows the change.

This is the biggest advantage of components.

---

## What Makes a Component "Reusable"?

A reusable component is:

* Written once.
* Used many times.
* Easy to maintain.
* Easy to update.

For example:

```
Button
```

Instead of creating a new button every time:

```jsx
<button>Save</button>

<button>Login</button>

<button>Register</button>

<button>Delete</button>
```

You create one Button component and reuse it wherever you need a button.

We'll learn how to customize it with props in a later lesson.

---

## Common Reusable Components

Most websites contain many reusable pieces.

Examples:

```
Navbar
```

Appears on almost every page.

#

```
Footer
```

Usually appears on every page.

#

```
Button
```

Used throughout the application.

#

```
Card
```

Displays products, blog posts, user profiles, and more.

#

```
Sidebar
```

Common in admin dashboards.

#

```
Modal
```

Used for dialogs and popups.

#

```
Search Box
```

Can be reused across different pages.

---

## Visual Example

Imagine an online shopping website.

```
Home Page
│
├── Navbar
├── Product Card
├── Product Card
├── Product Card
├── Product Card
└── Footer
```

Notice something?

The **Product Card** appears many times.

Instead of writing its HTML repeatedly, you create **one Product Card component** and display it for each product.

---

## Benefits of Reusable Components

### 1. Less Code

Write once.

Use many times.

#

### 2. Easier Maintenance

Need to fix a bug?

Update one component.

Every page benefits.

#

### 3. Consistent UI

Every button, card, or navbar looks and behaves the same.

#

### 4. Faster Development

Once a component exists, you can reuse it instead of rebuilding it.

#

### 5. Better Organization

Instead of one massive file:

```
Home Page
(800 lines)
```

You might have:

```
Home Page
│
├── Navbar
├── Hero
├── Features
├── Testimonials
└── Footer
```

Each part is smaller, easier to understand, and easier to maintain.

---

## When Should You Create a Component?

A good rule for beginners is:

If you find yourself copying the same UI into multiple places, it's a strong sign that it should become a reusable component.

Examples:

- ✅ Navigation bar
- ✅ Footer
- ✅ Product card
- ✅ User profile card
- ✅ Button

Examples that might stay inside a page:

* A unique hero section used only on the home page.
* A one-off layout that isn't reused anywhere else.

---

## Mini Exercise (No Coding Yet)

Look at these UI elements and decide whether they are good candidates for reusable components:

```
1. Navbar

2. Footer

3. Login Button

4. Product Card

5. Company Logo

6. Hero Banner that exists only on the Home page
```

For each one, answer:

* **Reusable Component?** (Yes/No)
* **Why?**

Don't worry about being perfect—this exercise is meant to build your intuition.

---

## Lesson Summary

Today we learned:

* ✅ What a reusable component is.
* ✅ Why components are important.
* ✅ The problem of duplicated code.
* ✅ The benefits of reusing UI.
* ✅ When you should create a component.

We **did not** discuss folder organization or where components should live. That is **Step 20** in our roadmap, and we'll cover it in the next lesson to keep our pace consistent.
