**Phase 7 — Data Fetching**

# Step 4 — Loading UI

So far, we've completed:

* ✅ Step 24 — Fetch Data from an API
* ✅ Step 25 — Server-side Fetching
* ✅ Step 26 — Client-side Fetching 

---

## Today's Goal

By the end of this lesson, you'll be able to answer:

* What is a Loading UI?
* Why is it necessary?
* What happens while data is being fetched?
* What does the user experience without a Loading UI?
* How does Next.js handle loading states?
* What is the purpose of `loading.tsx`?

We will **not** learn:

* Error UI (`error.tsx`) — that's **Step 28**.

Today is only about **Loading UI**.

---

## First Question

### What is a Loading UI?

Imagine you open this page:

```text
/products
```

The page needs to fetch **1,000 products** from a database.

Fetching the data takes **3 seconds**.

During those 3 seconds...

What should the user see?

#

### Option 1

A completely blank page.

```text
____________________
                    |
                    |
                    |
                    |
____________________|
```

#

### Option 2

A message like:

```text
Loading products...
```

#

### Option 3

A beautiful loading animation.

```text
Loading...

████░░░░░░
```

or

```text
████████

████████

████████
```

(skeleton placeholders)

Option 2 and Option 3 are examples of a **Loading UI**.

---

## Why Do We Need a Loading UI?

Computers are fast.

Networks are not always fast.

A request may take:

```text
50 ms

200 ms

1 second

5 seconds

10 seconds
```

The user doesn't know what's happening behind the scenes.

Without feedback, they might think:

* The website is broken.
* The button didn't work.
* The internet is disconnected.

A Loading UI tells the user:

> "Your request is being processed. Please wait."

---

## Real-Life Example

Imagine you're at a restaurant.

You order food.

The waiter says nothing.

Five minutes pass.

Ten minutes pass.

You'll probably wonder:

> "Did they forget my order?"

Now imagine the waiter says:

```text
Your food is being prepared.
```

You know everything is fine.

That's exactly what a Loading UI does.

---

## What Happens Without a Loading UI?

Let's follow the request.

```text
User opens /products
        │
        ▼
Browser requests page
        │
        ▼
Next.js fetches data
        │
        ▼
(Waiting...)
        │
        ▼
Products returned
        │
        ▼
Page displayed
```

During the **waiting** period...

The user sees nothing.

This creates a poor user experience.

---

## What Happens With a Loading UI?

The flow changes.

```text
User opens /products
        │
        ▼
Browser requests page
        │
        ▼
Loading UI appears
        │
        ▼
Next.js fetches data
        │
        ▼
Products returned
        │
        ▼
Loading UI disappears
        │
        ▼
Products displayed
```

Notice something important:

The data still takes the same amount of time to arrive.

The Loading UI doesn't make the application faster.

It simply gives the user feedback while they wait.

---

## What is `loading.tsx`?

In the **App Router**, Next.js provides a special file:

```text
loading.tsx
```

Its purpose is simple:

> Display temporary content while the page is loading.

Think of it like this:

```text
Page starts loading
        │
        ▼
loading.tsx
        │
        ▼
Data is fetched
        │
        ▼
page.tsx
```

The user first sees the Loading UI.

Once the data is ready, the real page replaces it.

---

## A Simple Folder Example

Suppose your application has:

```text
app/
│
├── products/
│   ├── page.tsx
│   └── loading.tsx
```

When someone visits:

```text
/products
```

The sequence is:

```text
Request arrives

↓

loading.tsx appears

↓

Next.js fetches data

↓

page.tsx is rendered

↓

loading.tsx disappears
```

---

## What Should a Good Loading UI Look Like?

A good Loading UI should:

* Tell the user that work is in progress.
* Match the layout of the final page.
* Avoid sudden layout changes.

For example:

If the final page has:

```text
Product Card

Product Card

Product Card
```

A loading version might show:

```text
██████████

██████████

██████████
```

These are called **skeleton loaders**.

They help users understand what content is coming.

---

## Common Types of Loading UI

### Text

```text
Loading...
```

#

### Spinner

```text
◌
```

(rotating animation)

#

### Progress Bar

```text
█████░░░░░
```

#

### Skeleton Screen

```text
████████████

████████████

████████████
```

Modern applications often prefer skeleton screens because they resemble the final layout.

---

## Important Concept

A Loading UI is **temporary**.

It appears only while the application is waiting for data.

Once the data arrives:

```text
Loading UI

↓

Removed

↓

Real Content
```

The Loading UI is never the final content.

---

## Visual Summary

```text
User Opens Page
        │
        ▼
Next.js Starts Fetching
        │
        ▼
loading.tsx
        │
        ▼
Waiting for Data
        │
        ▼
Data Ready
        │
        ▼
page.tsx
        │
        ▼
Browser Displays Content
```

---

## Today's Exercise

Without looking at your notes, answer these questions:

1. What is a Loading UI?
2. Why do applications need a Loading UI?
3. Does a Loading UI make data fetching faster?
4. What is the purpose of `loading.tsx`?
5. What happens after the data is ready?
6. What is the difference between a spinner and a skeleton loader?

If you can explain those answers confidently, you've completed **Step 27** of our roadmap. 

---

## Review of Phase 7 So Far

You now understand:

* ✅ What data fetching is.
* ✅ Server-side fetching.
* ✅ Client-side fetching.
* ✅ Loading UI.

Each topic builds on the previous one, just as we planned in the roadmap.

---

## Next Lesson (Step 5)

We will continue with the final lesson of **Phase 7**:

> **Error UI**

We'll answer:

* What happens if data fetching fails?
* Why do applications need an Error UI?
* What is the purpose of `error.tsx`?
* How does Next.js recover from errors?
* What does the request flow look like when an error occurs?

We'll focus **only** on Error UI before moving to the next phase.
