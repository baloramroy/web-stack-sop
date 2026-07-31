**Phase 3 — App Router**

# Step 4 — Layouts (`layout.tsx`)

## Today's Goal

By the end of this lesson, you'll be able to answer:

* What is a layout?
* Why do layouts exist?
* What is `layout.tsx`?
* What is `children`?
* How does Next.js apply layouts to pages?

That's it.

---

## The Problem

Imagine you're building a company website.

You have three pages:

```text
/

about

contact
```

Every page should look like this:

```text
---------------------------------------
            Company Logo
---------------------------------------
 Home | About | Contact
---------------------------------------

Page Content

---------------------------------------
        © 2026 My Company
---------------------------------------
```

Notice something?

The **logo**, **navigation**, and **footer** are exactly the same on every page.

Only the middle content changes.

---

## Without Layouts

If layouts didn't exist, every page would have to repeat the same code.

For example:

```text
Home Page

Logo

Navbar

Home Content

Footer
```

#

```text
About Page

Logo

Navbar

About Content

Footer
```

#

```text
Contact Page

Logo

Navbar

Contact Content

Footer
```

You're copying the same header and footer into every page.

This creates two problems:

* A lot of duplicate code.
* If you change the navigation, you must update every page.

---

## The Solution: Layouts

Instead of repeating shared UI everywhere, Next.js lets you define it once.

Think of a layout like a picture frame.

```
+--------------------------------------+
| Header                               |
+--------------------------------------+
|                                      |
|      Different page goes here        |
|                                      |
+--------------------------------------+
| Footer                               |
+--------------------------------------+
```

The frame stays the same.

Only the picture inside changes.

---

## What is `layout.tsx`?

A `layout.tsx` file defines **shared UI** for one or more pages.

Examples of shared UI:

* Header
* Navbar
* Sidebar
* Footer
* Company logo
* Dashboard menu

Anything that should stay the same across multiple pages belongs in a layout.

---

## The Root Layout

Every Next.js project starts with a root layout.

You'll find it here:

```text
src/
└── app/
    ├── layout.tsx
    └── page.tsx
```

This layout wraps **every page** in your application.

Think of it like the outermost container.

---

## Visualizing the Flow

Suppose you visit:

```text
/about
```

Next.js processes the request like this:

```text
Browser
      │
      ▼
layout.tsx
      │
      ▼
page.tsx
      │
      ▼
Browser
```

The layout is rendered first.

Then the page is placed inside it.

---

## What is `children`?

This is the most important part of today's lesson.

Inside `layout.tsx`, you'll usually see something like this:

```tsx
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>
        {children}
      </body>
    </html>
  );
}
```

Don't worry about the TypeScript syntax yet.

Focus only on:

```tsx
{children}
```

---

## Think of `children` as a Placeholder

Imagine you have an empty box.

```text
Header

--------------------

      EMPTY

--------------------

Footer
```

The empty space is `children`.

When someone visits:

```text
/
```

Next.js places the Home page into that empty space.

```text
Header

--------------------

Home Page

--------------------

Footer
```

#

If someone visits:

```text
/ about
```

The same layout is used.

```text
Header

--------------------

About Page

--------------------

Footer
```

#

If someone visits:

```text
/contact
```

Again:

```text
Header

--------------------

Contact Page

--------------------

Footer
```

The layout never changes.

Only `children` changes.

---

## Another Visualization

Think of a hotel.

Every room has the same:

* Walls
* Floor
* Door
* Ceiling

Only the guest changes.

```
Hotel Room
│
├── Bed
├── Window
├── Bathroom
└── Guest
```

The room is the layout.

The guest is `children`.

---

## How Pages Fit Into the Layout

Suppose your project looks like this:

```text
app/
├── layout.tsx
├── page.tsx
├── about/
│   └── page.tsx
└── contact/
    └── page.tsx
```

What happens?

```
layout.tsx
        │
        ├──────── Home Page
        │
        ├──────── About Page
        │
        └──────── Contact Page
```

One layout.

Many pages.

---

## Why Is This Better?

Imagine your navigation has 20 links.

Without layouts:

```
20 links

×

100 pages
```

You must update every page.

With layouts:

```
20 links

×

1 layout
```

Update once.

Every page automatically uses the new navigation.

---

## Django Comparison

If you've used Django templates, this idea should feel familiar.

In Django, you might have:

```text
base.html
```

and then:

```html
{% extends "base.html" %}
```

The page fills in blocks inside the base template.

In Next.js:

* `layout.tsx` is similar to `base.html`.
* `children` is similar to the content block that gets replaced.

It's not identical, but it's a helpful mental model because both let you define shared page structure.

---

## Rules to Remember

- `layout.tsx` defines shared UI.
- Every page inside that route uses the layout.
- `children` is where the page content is rendered.
- The root `layout.tsx` wraps the entire application.

---

## Mini Exercise

### Question 1

Which of these belongs in a layout?

* A. Company logo
* B. Navigation bar
* C. Footer
* D. All of the above

#

### Question 2

What does `children` represent?

* A. A CSS class
* B. The current page content
* C. The project folder
* D. The browser

#

### Question 3

Suppose you have:

```text
app/
├── layout.tsx
├── page.tsx
└── about/
    └── page.tsx
```

How many pages use `layout.tsx`?

---

## Lesson Summary

Today you learned one of the most important concepts in the App Router:

> **A layout provides shared UI, and `children` is the placeholder where the current page is rendered.**

This allows you to define common elements—such as headers, navigation bars, and footers—once and reuse them across many pages without duplication.

---

## Next Lesson (Step 5)

In the next lesson, we'll learn **Navigation**.

You'll discover:

* Why you shouldn't use a normal `<a>` tag for internal navigation.
* What the `Link` component is.
* How to move between pages.
* What happens when you click a link in a Next.js application.

This lesson naturally builds on what you've learned about pages and layouts, because navigation connects those pages together.
