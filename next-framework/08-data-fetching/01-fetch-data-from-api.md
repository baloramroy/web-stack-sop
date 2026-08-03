**Phase 7 — Data Fetching**

# Step 24: Fetch Data from an API

This phase is where your application starts working with **real data** instead of hardcoded text.

At the end of this phase, you'll understand:

* Where data comes from
* How Next.js fetches data
* When data is fetched
* What happens while data is loading
* What happens if fetching fails

But today, we will **only** study **Step 24**.

---

## Today's Goal

By the end of this lesson, you'll be able to answer:

* What is an API?
* Why do we need APIs?
* What is data fetching?
* Why does a Next.js application fetch data?
* What does `fetch()` do?
* What does a response look like?
* What is JSON?
* What happens from the moment a page requests data until it appears on the screen?

We are **not** learning:

* Server-side fetching
* Client-side fetching
* Loading UI
* Error handling

Those are separate lessons in this phase.

---

## Before We Write Any Code

Let's answer the most important question.

### What is Data Fetching?

Imagine you're building an online bookstore.

Your website has a page:

```
/books
```

Should you write this?

```text
Book 1
Book 2
Book 3
Book 4
```

inside your code?

No.

Why?

Because tomorrow a new book may be added.

Next week another one may be removed.

The information changes.

Instead, your website asks another system:

> "Can you give me the latest list of books?"

That process is called **data fetching**.

---

## Real Life Analogy

Imagine you're sitting in a restaurant.

You don't walk into the kitchen.

Instead:

```
You
 │
 ▼
Waiter
 │
 ▼
Kitchen
 │
 ▼
Food
 │
 ▼
Waiter
 │
 ▼
You
```

In a web application:

```
Browser
 │
 ▼
Next.js
 │
 ▼
API
 │
 ▼
Database
 │
 ▼
API
 │
 ▼
Next.js
 │
 ▼
Browser
```

Notice something important:

The browser **doesn't usually talk directly to the database**.

There is an API in between.

---

## What is an API?

API stands for:

**Application Programming Interface**

That's the formal name, but an easier way to think about it is:

> An API is a **messenger** that lets one application ask another application for information.

For example:

```
Weather App
      │
      ▼
Weather API
      │
      ▼
Weather Database
```

Or:

```
Shopping Website
        │
        ▼
Product API
        │
        ▼
Product Database
```

---

## What is Data?

Data is simply information.

Examples:

A user:

```json
{
  "name": "Baloram",
  "age": 31
}
```

A product:

```json
{
  "id": 1,
  "name": "Laptop",
  "price": 1200
}
```

A blog post:

```json
{
  "title": "Learning Next.js",
  "author": "John"
}
```

All of these are data.

---

## Where Does Data Come From?

Many beginners think Next.js "contains" the data.

Usually, it doesn't.

Data can come from:

```
Database

↓

API

↓

Next.js

↓

Browser
```

Or from another service:

```
GitHub API

↓

Next.js

↓

Browser
```

Or:

```
Weather API

↓

Next.js

↓

Browser
```

---

## What is `fetch()`?

JavaScript provides a built-in function called:

```javascript
fetch()
```

Its job is simple:

> "Go to this URL and bring back the data."

Think of it like ordering food:

```
fetch()

↓

Send request

↓

Wait

↓

Receive response

↓

Use the data
```

---

## A Typical Flow

Imagine your page needs a list of products.

The sequence looks like this:

```
User opens:

/products
        │
        ▼
Next.js starts rendering
        │
        ▼
Needs product data
        │
        ▼
Calls fetch()
        │
        ▼
API receives request
        │
        ▼
Database returns products
        │
        ▼
API sends JSON
        │
        ▼
Next.js receives data
        │
        ▼
Page is rendered
        │
        ▼
Browser displays products
```

---

## What is JSON?

Most APIs return data in **JSON (JavaScript Object Notation)**.

Example:

```json
[
  {
    "id": 1,
    "title": "Learn Next.js"
  },
  {
    "id": 2,
    "title": "Learn React"
  }
]
```

JSON is simply a structured way to represent data that different applications can exchange.

---

## Important Concept

A page has two main parts:

**Static Content**

This doesn't change often.

Example:

```text
Welcome to Our Store
```

**Dynamic Content**

This comes from data.

Example:

```text
Laptop
Mouse
Keyboard
Monitor
```

Data fetching is what allows the dynamic part to be updated.

---

## Visual Summary

```
User visits page
        │
        ▼
Next.js
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
Next.js
        │
        ▼
Browser
```

---

## Today's Exercise (No Next.js Yet)

Don't write any code today.

Instead, make sure you can explain these questions in your own words:

1. What is data fetching?
2. Why do websites fetch data instead of hardcoding everything?
3. What is an API?
4. What role does `fetch()` play?
5. What is JSON?
6. Why is an API usually placed between the application and the database?

If you can answer these comfortably, you've achieved the goal of **Step 24**.

---

## Next Lesson (Step 2)

We will **not** jump ahead today.

In the next lesson, we'll learn:

> **Server-side Fetching**

We'll answer questions such as:

* What does "server-side" mean in Next.js?
* Where does the code execute?
* Why is server-side fetching the default in the App Router?
* How does the request flow differ from client-side fetching?
* We'll write our **first real `fetch()` example** and trace exactly how the data travels from the API to the browser.

We'll continue following the roadmap one step at a time, without skipping ahead.
