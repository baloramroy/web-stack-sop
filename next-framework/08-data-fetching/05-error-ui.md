**Phase 7 — Data Fetching**

# Step 5 — Error UI

So far, we've completed all previous steps in **Phase 7 — Data Fetching**:

* ✅ Step 1 — Fetch Data from an API
* ✅ Step 2 — Server-side Fetching
* ✅ Step 3 — Client-side Fetching
* ✅ Step 4 — Loading UI

Today we begin the final lesson of this phase.



---

## Today's Goal

By the end of this lesson, you'll be able to answer:

* What is an Error UI?
* Why do applications need an Error UI?
* What happens when data fetching fails?
* What is the purpose of `error.tsx`?
* How does Next.js recover from errors?
* What is the request flow when an error occurs?

Today we'll only learn the **concept**. We won't write code yet.

---

## First Question

### What is an Error UI?

Imagine your application has a page:

```text
/products
```

Normally, the page fetches product data from an API.

Most of the time, everything works.

But what if something goes wrong?

For example:

* The API server is down.
* The database is unavailable.
* The internet connection is lost.
* The API returns an unexpected response.

Without handling these situations, the application may fail to display useful information.

An **Error UI** is what the user sees **instead of a broken page**.

---

## Why Do We Need an Error UI?

Imagine you're using an online banking website.

You click:

```text
View Transactions
```

The server has a temporary problem.

Without an Error UI, you might see:

```text
Something went wrong
```

or even a completely blank page.

That doesn't help you understand what happened.

A better experience would be:

```text
We couldn't load your transactions.

Please try again.
```

This is the purpose of an Error UI.

It communicates that:

* Something went wrong.
* The application knows about it.
* The user has guidance on what to do next.

---

## Real-Life Example

Imagine you're traveling by train.

Normally:

```text
Passenger

↓

Train arrives

↓

Journey continues
```

Now imagine the train has a mechanical problem.

Would the station simply lock all the doors and say nothing?

No.

Instead, an announcement is made:

```text
Train delayed.

Please wait.

We apologize for the inconvenience.
```

The announcement is the **Error UI**.

It doesn't fix the train.

It explains the situation and informs the passengers.

---

## What Happens Without an Error UI?

Suppose the page requests product data.

```text
User opens /products
        │
        ▼
Next.js fetches data
        │
        ▼
API fails
        │
        ▼
❌ Application crashes
```

The user may only see a confusing error.

---

## What Happens With an Error UI?

Now let's improve the flow.

```text
User opens /products
        │
        ▼
Next.js fetches data
        │
        ▼
API fails
        │
        ▼
error.tsx
        │
        ▼
Friendly error message
```

Instead of a broken experience, the user receives a meaningful message.

---

## What is `error.tsx`?

In the App Router, Next.js provides another special file:

```text
error.tsx
```

Its purpose is simple:

> Display an error page when something goes wrong while rendering a route.

Think of it like this:

```text
Request starts
        │
        ▼
Fetch data
        │
        ▼
Success?
   │          │
 Yes         No
   │          │
   ▼          ▼
page.tsx   error.tsx
```

Only one of them is shown to the user.

---

## A Folder Example

Suppose your application has:

```text
app/
│
├── products/
│   ├── page.tsx
│   ├── loading.tsx
│   └── error.tsx
```

When the request succeeds:

```text
/products

↓

loading.tsx

↓

page.tsx
```

When something fails:

```text
/products

↓

loading.tsx

↓

error.tsx
```

The user is not left staring at a blank screen.

---

## Does `error.tsx` Fix the Problem?

This is an important concept.

The answer is:

**No.**

`error.tsx` does **not** repair the API, restart the database, or restore the network.

Its job is to:

* Inform the user.
* Prevent the application from crashing visually.
* Offer a better user experience.

Think of it as a safety net.

---

## Recovering from Errors

Sometimes the problem is temporary.

For example:

* The API was restarting.
* The network briefly disconnected.
* The database was busy.

After a short time, everything works again.

A good application should allow the user to try again instead of forcing them to close the website.

Conceptually, the flow looks like this:

```text
User opens page
        │
        ▼
Request fails
        │
        ▼
error.tsx appears
        │
        ▼
User tries again
        │
        ▼
Request succeeds
        │
        ▼
page.tsx appears
```

We'll learn the implementation details later in the roadmap. Today, the important idea is that recovery is possible.

---

## Loading UI vs Error UI

Many beginners confuse these two.

| Loading UI                     | Error UI                                                    |
| ------------------------------ | ----------------------------------------------------------- |
| Appears while waiting for data | Appears when something fails                                |
| Temporary                      | Temporary until the problem is resolved or the user retries |
| Indicates progress             | Indicates failure                                           |
| Uses `loading.tsx`             | Uses `error.tsx`                                            |

A simple way to remember them:

* **Loading UI:** "Please wait."
* **Error UI:** "Something went wrong."

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
Did everything succeed?
      │           │
     Yes          No
      │           │
      ▼           ▼
 page.tsx    error.tsx
```

---

## Common Situations That Can Trigger an Error UI

Some examples include:

* The API server is unavailable.
* The database cannot be reached.
* The requested resource doesn't exist.
* An unexpected error occurs while rendering the page.

The exact cause doesn't matter to the user—they just need a clear and helpful experience.

---

## Today's Exercise

Without looking at your notes, answer these questions:

1. What is an Error UI?
2. Why is an Error UI important?
3. What is the purpose of `error.tsx`?
4. Does `error.tsx` fix the underlying problem?
5. What is the difference between `loading.tsx` and `error.tsx`?
6. What happens if a user retries after a temporary error?

If you can explain these confidently, you've completed **Step 28** of our roadmap. 

---

## 🎉 Phase 7 Completed

You have now completed:

* ✅ Step 1 — Fetch Data from an API
* ✅ Step 2 — Server-side Fetching
* ✅ Step 3 — Client-side Fetching
* ✅ Step 4 — Loading UI
* ✅ Step 5 — Error UI

You now understand the complete **data fetching lifecycle**:

```text
User Opens Page
        │
        ▼
Next.js Starts Request
        │
        ▼
Loading UI (loading.tsx)
        │
        ▼
Fetch Data
        │
        ├───────────────┐
        ▼               ▼
   Success            Failure
        │               │
        ▼               ▼
   page.tsx        error.tsx
```

This gives you a strong conceptual foundation before we move on to the next phase.

---

## Next Phase

Following our roadmap, the next phase is:

> **Phase 8 — Forms**

We'll start with **Step 1 — Create Forms**, where we'll answer:

* What is a form?
* Why do web applications use forms?
* What are the common HTML form elements?
* How does a user submit information?
* How do forms fit into the request–response cycle?

As always, we'll cover **one topic at a time** and maintain the same slow, structured pace.
