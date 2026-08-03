**Phase 7 — Data Fetching**

# Step 2 — Server-side Fetching

From the roadmap, we have completed:

* ✅ Step 24 — Fetch Data from an API 

---

## Today's Goal

By the end of this lesson, you should be able to answer:

* What is server-side fetching?
* Why is it the default in the Next.js App Router?
* Where does the code execute?
* When is the data fetched?
* What happens from the browser request until the page is displayed?
* What are the advantages of server-side fetching?

We will **not** learn today:

* Client-side fetching (Step 26)
* Loading UI (Step 27)
* Error UI (Step 28)

We'll stay focused on one topic.

---

## First Question

### What does "Server-side" mean?

Let's begin with a simple question.

Imagine your application is running at:

```text
http://localhost:3000
```

When someone visits:

```text
/products
```

Where should the application fetch the product data?

There are two possibilities.

### Option 1

The browser fetches the data.

```text
Browser
    │
    ▼
API
```

### Option 2

The server fetches the data.

```text
Browser
    │
    ▼
Next.js Server
    │
    ▼
API
```

Today we are learning **Option 2**.

This is called **server-side fetching**.

---

## What Does "Server-side" Actually Mean?

It simply means:

> The data is fetched by the Next.js server **before** the page is sent to the browser.

The browser does **not** contact the API directly.

Instead:

```text
Browser
    │
    ▼
Next.js Server
    │
    ▼
API
    │
    ▼
Database
```

The server collects everything it needs first.

Only then does it send the completed page back to the browser.

---

## Real-Life Example

Imagine you order food at a restaurant.

### Client-side

```text
You
 │
 ▼
Kitchen
```

You walk into the kitchen yourself.

#

### Server-side

```text
You
 │
 ▼
Waiter
 │
 ▼
Kitchen
 │
 ▼
Waiter
 │
 ▼
You
```

The waiter does the work for you.

In this analogy:

* **You** = Browser
* **Waiter** = Next.js Server
* **Kitchen** = API / Database

The browser simply asks for the page.

The Next.js server gathers the required data and returns a finished result.

---

## Request Flow

Suppose a user opens:

```text
/products
```

The request travels like this:

```text
Browser
    │
    ▼
Next.js Server
    │
    ▼
Needs product data
    │
    ▼
fetch()
    │
    ▼
API
    │
    ▼
Database
    │
    ▼
Products
    │
    ▼
API Response
    │
    ▼
Next.js Server
    │
    ▼
Build HTML
    │
    ▼
Browser
```

Notice an important point:

The browser doesn't receive "half a page."

It receives a page that already includes the fetched data.

---

## Where Does `fetch()` Execute?

This is one of the most important concepts in this lesson.

With **server-side fetching**:

```text
fetch()
```

runs on the **Next.js server**.

**Not** in the browser.

This means:

```text
Browser
```

doesn't execute the data request.

Instead:

```text
Next.js Server

↓

fetch()

↓

API
```

---

## Why Is This the Default in the App Router?

According to our roadmap, this is one of the key questions for Step 25. 

The App Router is designed so that pages can be rendered on the server first.

This provides several benefits:

* The browser gets a page that already contains the data.
* Initial page rendering is often faster because the browser doesn't need to wait for an extra API request after the page loads.
* Search engines can more easily see the rendered content.

For now, remember this simple rule:

> **In the App Router, think "server first."**

We'll explore exceptions later when we study **Client Components** and **client-side fetching**.

---

## A Simple Example

Imagine your API returns:

```json
[
  {
    "id": 1,
    "name": "Laptop"
  },
  {
    "id": 2,
    "name": "Keyboard"
  }
]
```

With server-side fetching, the sequence is:

```text
User opens page

↓

Next.js fetches products

↓

Next.js builds HTML

↓

Browser receives HTML

↓

Products are already visible
```

The browser doesn't need to make another request just to display the initial product list.

---

## Server-side vs Client-side (Preview)

We won't study client-side fetching until **Step 26**, but here's a quick comparison to prepare you.

| Server-side Fetching                 | Client-side Fetching                         |
| ------------------------------------ | -------------------------------------------- |
| Runs on the Next.js server           | Runs in the browser                          |
| Fetches data before sending the page | Fetches data after the page loads            |
| Browser receives HTML with data      | Browser loads page first, then requests data |

We'll go deeper into the second column in the next lesson.

---

## Visual Summary

```text
User visits /products
        │
        ▼
Next.js Server
        │
        ▼
fetch()
        │
        ▼
API
        │
        ▼
Database
        │
        ▼
JSON Response
        │
        ▼
Next.js Server builds HTML
        │
        ▼
Browser displays the page
```

---

## Today's Exercise

Without looking at your notes, try answering these questions:

1. What does **server-side fetching** mean?
2. Where does `fetch()` execute during server-side fetching?
3. Why doesn't the browser contact the API directly in this approach?
4. What is the role of the Next.js server?
5. Why is server-side fetching the default approach in the App Router?

If you can explain this flow in your own words, you've understood the core idea of **Step 25**.

---

## Next Lesson (Step 3)

We will continue according to the roadmap. 

The next lesson is:

> **Client-side Fetching**

We'll answer:

* What is client-side fetching?
* When should you use it?
* How is it different from server-side fetching?
* What changes in the request flow?
* Why do some pages still fetch data in the browser?

Only after you're comfortable with today's lesson will we move on to Step 3.
