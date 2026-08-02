**Phase 6 — Client & Server Components**

 Step 23: When Should You Use Server Components or Client Components?

This lesson connects everything you've learned in **Step 1** and **Step 2**.

We are **not** learning any new APIs today.

We are learning **how to think**.

---

## Learning Goal

By the end of today's lesson, you should be able to answer:

* How do I decide whether a component should be Server or Client?
* What questions should I ask before creating a component?
* Can one page contain both Server and Client Components?
* What is the recommended approach in Next.js?

---

## The Biggest Beginner Question

When people first learn Next.js App Router, they usually ask:

> "Should I make everything a Server Component or everything a Client Component?"

The answer is:

**Neither.**

Next.js encourages you to choose the right tool for each part of your UI.

---

## Think About Responsibilities

Instead of asking:

> "Server or Client?"

Ask:

> **"What is this component responsible for?"**

There are generally two responsibilities.

### 1. Display Information

Example:

```text
Company Name

About Us

Blog Article

Product Description

Terms & Conditions
```

The component's job is simply to **display** information.

These are usually good candidates for **Server Components**.

---

### 2. Handle User Interaction

Example:

```text
Login Form

Search Box

Shopping Cart

Like Button

Dark Mode Switch
```

The component's job is to **react to the user's actions**.

These are usually good candidates for **Client Components**.

---

## A Mental Model

Imagine you're building a library.

There are two employees.

### Employee 1

Works in the back office.

Responsibilities:

* Organize books
* Print reports
* Prepare information

Customers never interact directly with this employee.

This is like a **Server Component**.

#

### Employee 2

Works at the front desk.

Responsibilities:

* Answer questions
* Check out books
* Help visitors

This employee constantly interacts with people.

This is like a **Client Component**.

---

## Can They Work Together?

Yes.

In fact, **they usually do**.

Imagine a product page.

```text
Product Page
│
├── Product Information
├── Product Images
├── Product Description
├── Reviews
└── Add to Cart Button
```

Now think about each part.

#

### Product Information

```text
Product Name

Price

Description
```

Does the user interact with these?

No.

These are good **Server Components**.

#

### Add to Cart Button

The user clicks it.

The cart updates.

This should be a **Client Component**.

#

The page now looks like this.

```text
Product Page (Server)
│
├── Product Info (Server)
├── Description (Server)
├── Reviews (Server)
└── Add To Cart (Client)
```

Notice something important.

A **single page** can contain **both** Server and Client Components.

This is completely normal in Next.js.

---

## Another Example

Imagine a blog page.

```text
Blog Page
│
├── Navbar
├── Article
├── Author
├── Comments
└── Like Button
```

Let's decide.

#

### Article

The user reads it.

No interaction.

↓

Server Component

#

### Author Information

Just displays text.

↓

Server Component

#

### Like Button

User clicks.

↓

Client Component

#

### Comments

If comments are only displayed:

↓

Server Component

If users can type and submit comments:

↓

The comment form becomes a Client Component.

Notice that different parts of the same feature can have different responsibilities.

---

## Decision Flow

Whenever you create a component, ask yourself these questions.

```text
Does it only display information?
        │
       Yes
        │
        ▼
 Server Component
```

#

If the answer is:

```text
Does it respond to user interaction?
        │
       Yes
        │
        ▼
 Client Component
```

---

## Common Real-World Examples

| UI Element           | Recommendation | Why?                                  |
| -------------------- | -------------- | ------------------------------------- |
| About Page           | Server         | Mostly static content                 |
| Blog Article         | Server         | Read-only content                     |
| Product Details      | Server         | Displays product information          |
| Privacy Policy       | Server         | Static content                        |
| FAQ Page             | Server         | Displays information                  |
| Login Form           | Client         | User enters data                      |
| Search Input         | Client         | Responds to typing                    |
| Theme Toggle         | Client         | User interaction                      |
| Shopping Cart Button | Client         | Updates UI immediately                |
| Dropdown Menu        | Client         | Opens and closes based on user action |

---

## Common Beginner Mistakes

### Mistake 1

Making everything a Client Component.

```text
Navbar

Footer

About Page

Privacy Policy

Everything
```

Problem:

You're sending unnecessary JavaScript to the browser.

#

### Mistake 2

Making everything a Server Component.

Now imagine this.

```text
Login Form
```

User clicks.

Nothing happens.

Why?

Because interactive behavior belongs in the browser.

#

### Mistake 3

Thinking an entire page must be one type.

This is incorrect.

A page can contain:

```text
Server
│
├── Server
├── Server
├── Client
├── Server
└── Client
```

This is exactly how many real-world Next.js applications are built.

---

## Next.js Philosophy

The Next.js team encourages this mindset:

> **Keep components as Server Components by default.**

Then, **only use a Client Component when you actually need browser interaction.**

This approach gives you:

* Better performance
* Less JavaScript
* Faster page loads
* Better SEO

without sacrificing interactivity where it's needed.

---

## Real-World Scenario

Imagine you're building an online store.

Home page:

```text
Home
│
├── Navbar
├── Hero Banner
├── Featured Products
├── Categories
├── Newsletter Form
└── Footer
```

Let's classify them.

| Component         | Server or Client? | Reason                       |
| ----------------- | ----------------- | ---------------------------- |
| Hero Banner       | Server            | Displays content             |
| Featured Products | Server            | Shows product information    |
| Categories        | Server            | Displays navigation options  |
| Newsletter Form   | Client            | User enters an email address |
| Footer            | Server            | Static content               |

Notice that **only one part** of the page needs to be a Client Component.

That's a very common pattern.

---

## Key Takeaways

When building a component, don't start by asking:

> "Should this be Server or Client?"

Instead ask:

1. **What is this component's responsibility?**
2. **Does it only display information?**
3. **Does it need to respond to user interaction?**

The answers naturally guide your choice.

---

## Mini Exercise

For each component below, decide:

1. Server Component or Client Component?
2. Explain **why**.

| Component                                  | Your Choice | Why? |
| ------------------------------------------ | ----------- | ---- |
| Contact Us page                            | ?           | ?    |
| User Profile (display only)                | ?           | ?    |
| Edit Profile Form                          | ?           | ?    |
| Navigation Menu with dropdown              | ?           | ?    |
| Product Review List                        | ?           | ?    |
| Review Submission Form                     | ?           | ?    |
| Cookie Consent Banner with "Accept" button | ?           | ?    |
| Dashboard Statistics                       | ?           | ?    |

Don't worry about code yet. Focus only on the **responsibility** of each component.

---

## Lesson Summary

Today we learned:

* ✅ How to decide between Server and Client Components.
* ✅ That a single page can contain both types.
* ✅ Why responsibility is more important than the file itself.
* ✅ The "display vs interaction" decision process.
* ✅ The recommended Next.js philosophy: **Server by default, Client only when needed.**

---

## Roadmap Progress

* ✅ Phase 1 — Foundation
* ✅ Phase 2 — React Fundamentals
* ✅ Phase 3 — App Router
* ✅ Phase 4 — Styling
* ✅ Phase 5 — Components
* ✅ Phase 6 — Step 1: Understanding Server Components
* ✅ Phase 6 — Step 2: Understanding Client Components
* ✅ Phase 6 — Step 3: Choosing Between Server and Client Components

---

## Next Phase

The next phase in our roadmap is:

**Phase 7 — Data Fetching**

We'll begin with **Step 1: Fetching Data from an API**.
