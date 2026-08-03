**Phase 7 — Data Fetching**

# Step 3 — Client-side Fetching

From the roadmap, we have completed:

* ✅ Step 1 — Fetch Data from an API
* ✅ Step 2 — Server-side Fetching 

Today we begin:

---

## Today's Goal

By the end of this lesson, you'll be able to answer:

* What is client-side fetching?
* Where does the code execute?
* When does the browser fetch data?
* How is it different from server-side fetching?
* When should you choose client-side fetching?
* What are its advantages and disadvantages?

We will **not** learn today:

* Loading UI (Step 27)
* Error UI (Step 28)

We'll stay focused on client-side fetching only.

---

## First Question

### What is Client-side Fetching?

Client-side fetching means:

> The **browser** requests the data **after the page has already loaded**.

Unlike server-side fetching, the Next.js server does **not** fetch the data first.

Instead, the browser is responsible for asking the API.

---

## Compare the Two Approaches

### Server-side Fetching (Previous Lesson)

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
    │
    ▼
Next.js Server
    │
    ▼
Browser
```

The browser receives a page that already contains the data.

#

### Client-side Fetching

```text
Browser
    │
    ▼
Next.js Server
    │
    ▼
HTML Page
    │
    ▼
Browser
    │
    ▼
API
    │
    ▼
Database
    │
    ▼
Browser Updates UI
```

Notice the difference:

The browser makes the API request **after** it receives the page.

---

## Real-Life Analogy

Imagine you book a hotel room.

### Server-side

The hotel prepares everything before you arrive.

```text
Reception

↓

Checks reservation

↓

Prepares room

↓

Hands you the key
```

When you enter the room, everything is ready.

#

### Client-side

The hotel gives you the room immediately.

After entering, you request extra services.

```text
Enter room

↓

Call room service

↓

Request towels

↓

Wait

↓

Receive towels
```

The room is available quickly, but some information or services arrive later.

---

## Where Does `fetch()` Execute?

This is the most important concept in today's lesson.

With **client-side fetching**:

```javascript
fetch()
```

runs in the **browser**.

Not on the Next.js server.

The flow becomes:

```text
Browser

↓

fetch()

↓

API

↓

Database

↓

JSON Response

↓

Browser Updates Page
```

The Next.js server is no longer responsible for retrieving that data.

---

## What Does the User Experience?

Imagine a page that displays products.

### Server-side Fetching

The user opens:

```text
/products
```

They immediately see:

```text
Laptop

Keyboard

Mouse
```

because the data was already fetched before the page was sent.

#

### Client-side Fetching

The user opens:

```text
/products
```

Initially, they might see:

```text
Loading...
```

Then the browser fetches the data.

Finally, the page updates to:

```text
Laptop

Keyboard

Mouse
```

This delay is a normal part of client-side fetching.

---

## Request Flow

Let's follow the entire process.

```text
User visits /products
        │
        ▼
Next.js Server
        │
        ▼
Sends HTML
        │
        ▼
Browser Displays Page
        │
        ▼
Browser Runs JavaScript
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
Browser Updates UI
```

Notice that the browser has **two jobs**:

1. Display the page.
2. Fetch additional data and update the UI.

---

## When Should You Use Client-side Fetching?

Client-side fetching is useful when the data changes frequently or depends on the current user.

Some common examples are:

### Dashboard

```text
CPU Usage

Memory Usage

Active Users
```

These values change every few seconds.

#

### Notifications

```text
🔔 You have 3 new notifications
```

The browser can periodically check for new notifications.

#

### Live Chat

```text
Alice: Hi!

Bob: Hello!
```

Messages appear while the user is already on the page.

#

### Stock Prices

```text
Apple

Google

Microsoft
```

Prices change continuously.

---

## When Is Server-side Better?

If the content should already be available when the page loads, server-side fetching is usually a better choice.

Examples:

* Blog posts
* Product details
* Documentation
* News articles

The user expects the content to be visible immediately.

---

## Server-side vs Client-side

| Server-side Fetching                    | Client-side Fetching                             |
| --------------------------------------- | ------------------------------------------------ |
| Runs on the Next.js server              | Runs in the browser                              |
| Data is fetched before sending the page | Data is fetched after the page loads             |
| Browser receives HTML with data         | Browser receives HTML first, then requests data  |
| Good for initial page content           | Good for interactive or frequently changing data |

---

## One Important Rule

Many beginners think:

> "Client-side fetching is newer, so I should always use it."

That's not true.

Similarly, it's also incorrect to think:

> "Server-side fetching is always better."

The correct approach is:

* Use **server-side fetching** when the initial page should already contain the data.
* Use **client-side fetching** when the browser needs to keep updating or personalize data after the page has loaded.

Choosing the right approach depends on the problem you're solving.

---

## Visual Summary

```text
User Opens Page
        │
        ▼
Next.js Sends HTML
        │
        ▼
Browser Displays Page
        │
        ▼
Browser Calls API
        │
        ▼
Database
        │
        ▼
JSON Response
        │
        ▼
Browser Updates UI
```

---

## Today's Exercise

Without looking at your notes, answer these questions:

1. What is client-side fetching?
2. Where does `fetch()` execute?
3. Why does the browser sometimes show "Loading..."?
4. What is the main difference between server-side and client-side fetching?
5. Give two examples where client-side fetching is the better choice.
6. Give two examples where server-side fetching is the better choice.

If you can answer those questions confidently, you've completed **Step 26** of our roadmap. 

---

## Next Lesson (Step 4)

Following the roadmap, the next lesson will be:

> **Loading UI**

We'll learn:

* Why loading states are necessary.
* What users experience while waiting for data.
* How Next.js provides loading feedback.
* How a good loading UI improves user experience.
* The request flow during loading.

As always, we'll cover **only that single topic** before moving on.
