**Phase 6 — Client & Server Components**

# Step 1: Understanding Server Components

This is one of the biggest reasons Next.js is different from a normal React application.

**Today's lesson is only about understanding the idea.**


---

## Learning Goal

By the end of today's lesson, you should be able to answer:

* What is a Server Component?
* Why did Next.js introduce Server Components?
* Where does a Server Component run?
* What gets sent to the browser?
* What are the advantages of Server Components?

That's all.

---

## Before Next.js

In a traditional React application, the browser does almost all the work.

Imagine this flow:

```text
Browser
    │
    ▼
Downloads JavaScript
    │
    ▼
Runs React
    │
    ▼
Creates HTML
    │
    ▼
Displays the page
```

The browser is responsible for creating the user interface.

---

## The Problem

Imagine your application is very large.

For example:

```text
Dashboard

↓

20 Components

↓

Thousands of lines of JavaScript
```

The browser has to:

* Download all the JavaScript.
* Execute it.
* Build the page.

This can slow down the initial page load, especially on slower devices or networks.

---

## Next.js Has a Different Idea

Instead of asking the browser to build everything, Next.js can build parts of the page **on the server first**.

The flow becomes:

```text
Browser

↓

Request Page

↓

Next.js Server

↓

Creates HTML

↓

Sends HTML

↓

Browser Displays Page
```

Notice something?

The browser receives ready-made HTML instead of having to build everything from JavaScript.

---

## What Is a Server Component?

A **Server Component** is a React component that runs on the **server**, not in the user's browser.

Think of it like a chef in a restaurant.

### Without a chef

You receive:

```text
Raw ingredients

↓

You cook

↓

You eat
```

You do all the work.

#

### With a chef

You receive:

```text
Finished meal

↓

You eat
```

The cooking was already done.

#

A Server Component works the same way.

Instead of sending instructions for the browser to build the UI, the server prepares it first.

---

## Visual Flow

Imagine visiting:

```text
http://localhost:3000
```

The request looks like this:

```text
Browser

↓

Request "/"

↓

Next.js Server

↓

Runs Server Components

↓

Creates HTML

↓

Returns HTML

↓

Browser Displays Page
```

The browser doesn't need to build that part of the interface itself.

---

## Where Does It Run?

A Server Component runs:

```text
✓ On the Next.js server
```

It does **not** run:

```text
✗ In Chrome

✗ In Firefox

✗ In Edge

✗ On the user's computer
```

The server does the work before sending the result.

---

## What Does the Browser Receive?

The browser receives:

```text
HTML
```

Not the component itself.

Think of it like ordering a printed document.

The server prints the document and sends it to you.

You receive the finished pages, not the printer.

---

## Why Is This Useful?

Suppose your page shows:

* Company information
* Product catalog
* Blog article
* News page

These are mostly things the user wants to **read**.

There's no need for the browser to spend time generating them if the server can do it first.

---

## Benefits of Server Components

### 1. Faster Initial Load

The browser receives ready-to-display HTML.

---

### 2. Less JavaScript

Less JavaScript needs to be downloaded and executed.

---

### 3. Better Performance

The server performs part of the work, reducing the browser's workload.

---

### 4. Better SEO

Search engines can easily read server-generated HTML.

---

### 5. Better Security

Some logic and sensitive operations can stay on the server instead of being exposed to the browser.

> We'll explore this more when we discuss data fetching and authentication.

---

## Are All Components Server Components?

In the **App Router**, every component is a **Server Component by default**.

That's an important point.

If you create a component like this:

```tsx
export default function Home() {
  return <h1>Welcome</h1>;
}
```

Next.js treats it as a **Server Component** unless you explicitly tell it otherwise.

We'll learn how to change that in the next lesson.

---

## Mental Model

Think of a newspaper.

The newspaper company:

```text
Writes articles

↓

Prints newspaper

↓

Delivers newspaper

↓

Reader reads it
```

The reader doesn't print the newspaper.

The company already did that work.

A Server Component is similar.

The server prepares the UI before sending it to the browser.

---

## Real-World Examples

These are good candidates for Server Components:

```text
Home Page

About Page

Blog Article

Product Details

Documentation

Company Information

Terms & Conditions
```

These pages mainly display content, making server-side rendering a great fit.

---

## What We Are NOT Learning Today

To keep our pace slow and consistent, we're **not** covering:

* Why `useState` doesn't work in Server Components.
* Why `onClick` doesn't work in Server Components.
* The `"use client"` directive.
* Client Components.
* Interactive UI.

Those are all part of **Step 22**.

---

## Mini Exercise (No Coding Yet)

For each page below, decide whether it is a good candidate for a **Server Component** based on today's understanding.

| Page                 | Good Server Component? | Why? |
| -------------------- | ---------------------- | ---- |
| Company About page   | ?                      | ?    |
| Blog article         | ?                      | ?    |
| Product details page | ?                      | ?    |
| Documentation page   | ?                      | ?    |
| Privacy Policy page  | ?                      | ?    |

Don't worry about interactive pages yet—we haven't learned Client Components, so we'll evaluate those in the next lesson.

---

## Lesson Summary

Today we learned:

* ✅ What a Server Component is.
* ✅ Where Server Components run.
* ✅ How the request flows through the server.
* ✅ Why Next.js introduced Server Components.
* ✅ The benefits of server-side rendering in the App Router.
* ✅ That components are Server Components by default unless you opt into client-side behavior.

---

## Roadmap Progress

* ✅ Phase 1 — Foundation
* ✅ Phase 2 — React Fundamentals
* ✅ Phase 3 — App Router
* ✅ Phase 4 — Styling
* ✅ Phase 5 — Components
* ✅ Phase 6 — Step 1: Understanding Server Components

### Next Lesson

**Phase 6 — Step 2: Understanding Client Components**

We'll compare Server Components and Client Components, learn what `"use client"` means, and understand **when** you need a Client Component. We won't rush into hooks or advanced topics until that foundation is clear.
