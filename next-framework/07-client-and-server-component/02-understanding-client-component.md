**Phase 6 — Client & Server Components**

# Step 2: Understanding Client Components

Today we'll learn the second half of one of Next.js's most important concepts.

To keep our roadmap consistent, we'll **only** cover:

* What is a Client Component?
* Why do Client Components exist?
* What does `"use client"` mean?
* When should you use a Client Component?
* How is it different from a Server Component?


---

# Learning Goal

By the end of today's lesson, you should be able to answer:

* What is a Client Component?
* Where does it run?
* Why does Next.js need Client Components?
* What does `"use client"` actually do?
* When should you choose a Client Component instead of a Server Component?

---

# First, Let's Compare

From the previous lesson:

```text
Browser

↓

Request Page

↓

Next.js Server

↓

Server Component

↓

HTML

↓

Browser
```

The server prepares the page.

Now let's see a Client Component.

```text
Browser

↓

Downloads JavaScript

↓

Runs Component

↓

Updates UI
```

The browser is responsible for running the component.

---

# What Is a Client Component?

A **Client Component** is a React component that runs **inside the user's browser**.

Think of it like a TV remote.

The TV is already displaying a picture.

When you press:

* Volume Up
* Volume Down
* Channel Change

The remote immediately changes the TV.

You don't send a request to the TV manufacturer every time you press a button.

The interaction happens locally.

A Client Component works in the same way.

---

# Where Does It Run?

A Client Component runs:

```text
✓ Chrome

✓ Firefox

✓ Edge

✓ Safari

✓ User's browser
```

It does **not** execute on the Next.js server after the page has been delivered to the browser.

---

# Why Do We Need Client Components?

Imagine a button.

```text
[ Like ]
```

When you click it,

the page should react immediately.

Another example:

```text
Search Box
```

As you type,

the results change.

Or:

```text
Dark Mode Toggle
```

Click.

Theme changes instantly.

These are **interactive** features.

A Server Component cannot respond to browser events after the page is rendered.

That's where Client Components come in.

---

# What Does `"use client"` Mean?

By default, components in the App Router are **Server Components**.

If you want a component to run in the browser, you must tell Next.js.

You do that by placing this at the top of the file:

```tsx
"use client";
```

Think of it as a label.

```text
This component should run
inside the browser.
```

That's all it means.

It doesn't create a component.

It doesn't add new features.

It simply tells Next.js **where** the component should execute.

---

# Visual Comparison

## Server Component

```text
Browser

↓

Request

↓

Next.js Server

↓

Component Runs

↓

HTML

↓

Browser
```

---

## Client Component

```text
Browser

↓

Downloads JavaScript

↓

Component Runs

↓

User Clicks

↓

UI Updates
```

---

# Real-World Examples

Good examples of Client Components:

```text
Login Form

Search Box

Shopping Cart Counter

Theme Switch

Dropdown Menu

Image Carousel

Modal

Tabs

Accordion
```

Why?

Because users interact with them.

---

# A Restaurant Analogy

Imagine you're dining at a restaurant.

### Server Component

The chef:

* Cooks the meal.
* Plates it.
* Sends it to your table.

You simply receive it.

---

### Client Component

Now imagine you have a hotpot on your table.

You can:

* Add vegetables.
* Stir the soup.
* Adjust the heat.
* Cook more ingredients.

The interaction happens **at your table**.

That's like a Client Component.

The user can interact with it directly in the browser.

---

# Server vs Client

| Server Component            | Client Component                 |
| --------------------------- | -------------------------------- |
| Runs on the server          | Runs in the browser              |
| Default in App Router       | Requires `"use client"`          |
| Good for displaying content | Good for interactive UI          |
| Sends HTML                  | Downloads JavaScript and runs it |

---

# Should Everything Be a Client Component?

No.

A common beginner mistake is thinking:

> "If Client Components are interactive, I'll make every component a Client Component."

That would defeat one of the biggest advantages of Next.js.

Use a Client Component **only when the browser needs to do something after the page is displayed**.

If a page simply displays content, a Server Component is usually the better choice.

---

# Simple Decision Rule

Ask yourself one question:

> **Does this component need to respond to user interaction in the browser?**

If **No**:

```text
Server Component
```

If **Yes**:

```text
Client Component
```

This rule won't cover every advanced case, but it's an excellent guideline while you're learning.

---

# Mini Exercise (No Coding Yet)

For each UI element below, decide whether it is better as a **Server Component** or a **Client Component**, and explain why.

| UI Element           | Server or Client? | Why? |
| -------------------- | ----------------- | ---- |
| Company About page   | ?                 | ?    |
| Privacy Policy       | ?                 | ?    |
| Login Form           | ?                 | ?    |
| Search Box           | ?                 | ?    |
| Theme Toggle         | ?                 | ?    |
| Blog Article         | ?                 | ?    |
| Product Details page | ?                 | ?    |

Focus only on what you've learned today: **Does it need browser interaction?**

---

# Lesson Summary

Today we learned:

* ✅ What a Client Component is.
* ✅ Where Client Components run.
* ✅ Why interactive UI needs Client Components.
* ✅ What `"use client"` means.
* ✅ How Client Components differ from Server Components.
* ✅ A simple way to decide between the two.

---

## Roadmap Progress

* ✅ Phase 1 — Foundation
* ✅ Phase 2 — React Fundamentals
* ✅ Phase 3 — App Router
* ✅ Phase 4 — Styling
* ✅ Phase 5 — Components
* ✅ Phase 6 — Step 21: Understanding Server Components
* ✅ Phase 6 — Step 22: Understanding Client Components

### Next Lesson

We'll continue with **Phase 6 — Step 3: When Should You Use Server Components or Client Components?**

Instead of learning new syntax, we'll practice making good architectural decisions through real-world scenarios. This lesson ties together Steps 21 and 22 before we move on to data fetching and other advanced topics.
