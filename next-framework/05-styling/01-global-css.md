**Phase 4 — Styling**

# Step 16 — Global CSS


## Lesson Goal

By the end of this lesson, you'll be able to answer:

* What is CSS?
* What is Global CSS?
* Why does Next.js have a `globals.css` file?
* When should we use Global CSS?
* When should we **not** use Global CSS?

We're **not** learning CSS itself in depth today. We're only learning how **Next.js uses Global CSS**.

---

## Before We Start

Open your project in VS Code.

Your project should look similar to this:

```text
my-first-next-app/
│
├── src/
│   └── app/
│       ├── globals.css
│       ├── layout.tsx
│       └── page.tsx
│
├── public/
├── package.json
└── ...
```

Today we only care about one file:

```text
src/app/globals.css
```

---

## What is CSS?

CSS stands for:

> **Cascading Style Sheets**

HTML gives a page its **structure**.

CSS gives a page its **appearance**.

Example:

Without CSS

```text
Hello World
```

With CSS

```text
Hello World
```

* Blue color
* Large font
* Centered
* Background color
* Padding
* Rounded corners

CSS controls how your application looks.

---

## What is Global CSS?

Global CSS means:

> CSS rules that apply to the **entire application**.

Think of it like painting the walls of an entire house.

If you paint the whole house white,

every room gets white walls.

Global CSS works the same way.

---

## Where is Global CSS?

In a new Next.js project you'll find:

```text
src/app/globals.css
```

Open it.

You'll see something similar to:

```css
@import "tailwindcss";

:root {
  --background: #ffffff;
  --foreground: #171717;
}

body {
  background: var(--background);
  color: var(--foreground);
  font-family: Arial, Helvetica, sans-serif;
}
```

*(The exact contents may vary slightly depending on the Next.js version.)*

Don't worry about every line today.

We're only interested in **what this file is for**.

---

## How Does Next.js Use It?

Open:

```text
layout.tsx
```

You'll see something like:

```tsx
import "./globals.css";
```

This is very important.

That single line tells Next.js:

> "Load these styles for the whole application."

Every page automatically gets these styles because every page uses the root layout.

---

## Request Flow

Here's where `globals.css` fits in:

```text
Browser
      │
      ▼
page.tsx
      │
      ▼
layout.tsx
      │
      ▼
imports globals.css
      │
      ▼
CSS is applied
      │
      ▼
Browser displays the styled page
```

Notice that `globals.css` isn't loaded by each page individually. It's loaded once by the root layout and then shared across the application.

---

## What Belongs in Global CSS?

Global CSS is best for styles that should be consistent everywhere.

Examples:

```css
body {
    margin: 0;
}
```

```css
body {
    font-family: Arial, sans-serif;
}
```

```css
* {
    box-sizing: border-box;
}
```

```css
html {
    scroll-behavior: smooth;
}
```

These affect the whole application, which is exactly what Global CSS is for.

---

## What Should NOT Go in Global CSS?

Imagine you have a button on one page.

```text
Save
```

You want only that button to be green.

Don't do this:

```css
button {
    background: green;
}
```

Now **every** button in your application becomes green.

Instead, styles for a specific component should stay with that component. We'll learn that in the next lesson when we cover **CSS Modules**.

---

## Real-World Analogy

Imagine you're designing an office building.

### Global CSS

Building-wide rules:

* White walls
* Same company font
* Same floor tiles
* Same lighting

Every room follows these rules.

#

### CSS Modules (Next Lesson)

Individual room decoration:

* CEO office
* Meeting room
* Reception

Each room can look different without affecting the others.

---

## Why Not Put Everything in Global CSS?

Suppose you build a large application.

You create:

* Home page
* Dashboard
* Profile
* Settings
* Admin panel

If every style is placed into one `globals.css` file:

```text
globals.css
```

it becomes:

* Thousands of lines long
* Hard to maintain
* Easy to accidentally change styles on unrelated pages
* Difficult for teams to work on simultaneously

That's why we keep Global CSS for application-wide styles only.

---

## Today's Key Takeaways

* CSS controls the appearance of your application.
* `globals.css` contains styles shared by the entire application.
* The root `layout.tsx` imports `globals.css`.
* Every page receives those styles automatically.
* Use Global CSS only for styles that truly belong to the whole application.
* Avoid putting component-specific styles into `globals.css`.

---

## Practice (15–20 Minutes)

Don't build anything new today. Focus on observing and making small changes.

1. Open `src/app/globals.css`.
2. Find the `body` rule.
3. Change the `font-family` to another common font (for example, `Georgia` or `Verdana`).
4. Save the file and watch the browser update automatically.
5. Change the background color of the `body`.
6. Change the text color.
7. Restore the original styles when you're done experimenting.

The goal is to see that **one file changes the appearance of the entire application**.

---