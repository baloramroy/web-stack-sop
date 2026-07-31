**Phase 3 — App Router**

# Step 15 — Navigation with `Link`

## Today's Goal

By the end of this lesson, you'll be able to answer:

* Why do we need navigation?
* Why shouldn't we use a normal `<a>` tag?
* What is the `Link` component?
* How does Next.js navigate between pages?
* What happens behind the scenes when a user clicks a link?

That's it.

---

## The Problem

Imagine you've created three pages.

```text
/
```

Home page

```text
/about
```

About page

```text
/contact
```

Contact page

Now ask yourself:

> **How does a user move from one page to another?**

They need links.

---

## The Traditional HTML Way

In plain HTML, you would write:

```html
<a href="/about">About</a>
```

When the user clicks it:

```text
Browser
      │
      ▼
Request /about
      │
      ▼
Server
      │
      ▼
Entire page reloads
```

Everything reloads.

The browser throws away the current page and requests a completely new one.

---

## Why Is That a Problem?

Imagine this sequence:

```text
Home

↓

About

↓

Contact

↓

Home
```

If every click reloads the entire website:

* Slower navigation
* More waiting
* Less smooth user experience

Modern web applications try to avoid full page reloads whenever possible.

---

## The Next.js Way

Instead of using:

```html
<a href="/about">
```

Next.js provides a special component:

```tsx
<Link href="/about">
```

Think of `Link` as a smarter version of the HTML `<a>` tag.

It still takes the user to another page, but it does so more efficiently.

---

## What Does `Link` Do?

When you click a `Link`:

```text
Current Page
      │
      ▼
Next.js Router
      │
      ▼
Load only the new page content
      │
      ▼
Update the browser
```

Notice what's missing?

There is **no full page refresh**.

Only the page content changes.

---

## Visualizing the Difference

### Using `<a>`

```text
Home Page
      │
      ▼
Click About
      │
      ▼
Everything Reloads
      │
      ▼
About Page
```

#

### Using `Link`

```text
Home Page
      │
      ▼
Click About
      │
      ▼
Only Page Content Changes
      │
      ▼
About Page
```

The navigation feels much faster.

---

## A Real-World Analogy

Imagine you're reading a book.

### Using `<a>`

Every time you want the next chapter:

* Close the book.
* Put it back on the shelf.
* Take it again.
* Open it.

That's a lot of unnecessary work.

#

### Using `Link`

Simply turn the page.

The book stays in your hands.

That's what Next.js is trying to achieve.

---

## How It Fits with Layouts

Remember the previous lesson.

Your application might look like:

```text
--------------------------------
Logo

Navigation

-------------------------------

Current Page

-------------------------------

Footer
```

Suppose you're on:

```text
/
```

and click:

```text
About
```

With `Link`, Next.js keeps:

* ✅ Logo
* ✅ Navigation
* ✅ Footer

Only the middle section changes.

```text
--------------------------------
Logo

Navigation

-------------------------------

About Page

-------------------------------

Footer
```

This is one reason layouts and `Link` work so well together.

---

## A Simple Example

Suppose you have:

```text
/
```

and

```text
/about
```

A navigation link would look like:

```tsx
import Link from "next/link";

export default function HomePage() {
  return (
    <div>
      <Link href="/about">About</Link>
    </div>
  );
}
```

Let's focus on only one line:

```tsx
<Link href="/about">
```

This tells Next.js:

> "When the user clicks this, navigate to `/about`."

---

## What is `href`?

You've probably seen `href` before in HTML.

It simply means:

> **Where should this link go?**

Examples:

```text
/about
```

```text
/contact
```

```text
/products
```

The same idea applies to the `Link` component.

---

## Internal vs External Links

There is an important rule.

### Internal pages

Pages inside your Next.js application:

```text
/
```

```text
/about
```

```text
/contacts
```

Use:

```tsx
<Link>
```

#

### External websites

```text
https://google.com
```

```text
https://github.com
```

Use a normal HTML link:

```html
<a>
```

This is because Next.js can only optimize navigation **inside your own application**.

---

## Behind the Scenes

Suppose the user clicks:

```text
/products
```

Next.js roughly follows this flow:

```text
Current Page
      │
      ▼
Link Clicked
      │
      ▼
Next.js Router
      │
      ▼
Find page.tsx
      │
      ▼
Render New Page
      │
      ▼
Update Browser
```

Notice that the browser itself is not doing a full reload.

Next.js is handling the navigation.

---

## Django Comparison

In Django templates, you might write:

```html
<a href="{% url 'about' %}">About</a>
```

Clicking that link usually causes the browser to request a brand-new page from the server.

In a Next.js application using `Link`, navigation between pages is typically handled on the client, making it feel much more like a desktop application.

---

## Rules to Remember

- Use `Link` for pages inside your Next.js application.
- Use `<a>` for external websites.
- `href` specifies the destination.
- `Link` provides smoother navigation because it avoids a full page reload for internal routes.

---

## Mini Exercise

### Question 1

Which component should you use to navigate from:

```text
/
```

to

```text
/about
```

* A. `<a>`
* B. `Link`

#

### Question 2

Which should you use for:

```text
https://github.com
```

* A. `<a>`
* B. `Link`

#

### Question 3

When you click a `Link` inside a Next.js application, what usually happens?

* A. The entire website reloads.
* B. Only the necessary page content is updated.

---

## Phase 3 Completed! 🎉

Congratulations! You've now completed the **App Router Fundamentals**.

You understand:

* ✅ Pages (`page.tsx`)
* ✅ Basic Routing
* ✅ Nested Routes
* ✅ Dynamic Routes (`[id]`)
* ✅ Layouts (`layout.tsx`)
* ✅ Navigation with `Link`

These are the core building blocks of how users move through a Next.js application.

---

## What's Next?

The next phase in our roadmap is **Phase 4 — Styling**.



