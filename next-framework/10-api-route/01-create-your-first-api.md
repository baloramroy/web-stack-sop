**Phase 9 — API Routes**

# Step 1 - Create Your First API

Learn only:

```text
GET
```

Goal:

```text
Browser / Client

        │
        ▼

Next.js API Route

        │
        ▼

Return JSON

        │
        ▼

Browser / Client
```

That's it.

No database.

No POST.

No PUT.

No DELETE.

No authentication.

Just understand **how a GET API works in Next.js**.

---

## Before We Write Code

Up until now, everything we've built has been a **web page**.

For example:

```
http://localhost:3000/
```

returns

```html
<h1>Home Page</h1>
```

A browser knows how to display HTML.

---

An API is different.

Instead of returning HTML, it usually returns **data**.

Example:

```
GET /api/user
```

returns

```json
{
  "name": "Baloram",
  "role": "Student"
}
```

Notice:

* No HTML
* No CSS
* No React UI

Just data.

---

## What is an API?

Think of an API as a waiter in a restaurant.

```
Customer
      │
      ▼
Waiter (API)
      │
      ▼
Kitchen
      │
      ▼
Waiter
      │
      ▼
Customer
```

The customer doesn't go into the kitchen.

The waiter takes the request, gets the result, and brings it back.

An API plays the same role between a client (browser, mobile app, or another application) and your server logic.

---

## Where Does an API Live in Next.js?

In the App Router, API routes are created under the `app/api` directory.

A typical structure looks like this:

```text
src/
└── app/
    ├── page.tsx
    └── api/
        └── hello/
            └── route.ts
```

Notice something important:

```
page.tsx
```

creates a **web page**.

Whereas:

```
route.ts
```

creates an **API endpoint**.

This distinction is the key idea for today's lesson.

---

## How a GET Request Flows

When someone visits:

```
http://localhost:3000/api/hello
```

the flow is:

```text
Browser

      │

GET /api/hello

      │

Next.js App Router

      │

route.ts

      │

Return JSON

      │

Browser
```

This is very similar to what you learned earlier with pages, except the destination is a `route.ts` file instead of a `page.tsx`.

---

## Compare a Page and an API

| Page                               | API                                           |
| ---------------------------------- | --------------------------------------------- |
| `page.tsx`                         | `route.ts`                                    |
| Returns HTML/React                 | Returns data (usually JSON)                   |
| Displayed in the browser as a page | Consumed by browsers, apps, or other services |
| Used for UI                        | Used for data                                 |

---

## Why Do We Need APIs?

Imagine you're building a Task Manager application.

The page needs a list of tasks.

Instead of hardcoding them into the page, the page can ask an API:

```text
GET /api/tasks
```

The API responds with:

```json
[
  {
    "id": 1,
    "title": "Learn Next.js"
  },
  {
    "id": 2,
    "title": "Practice API Routes"
  }
]
```

The page then displays those tasks.

This separation keeps your UI and your data logic independent.

---

## Today's Learning Objective

By the end of this lesson, you should be able to answer:

* What is an API?
* What is the difference between a web page and an API?
* Why do APIs usually return JSON instead of HTML?
* Where are API routes created in a Next.js App Router project?
* What is the purpose of `route.ts`?
* What happens when a browser sends a `GET` request to an API route?

---

## What We Are **Not** Learning Today

To stay consistent with our roadmap, we will **not** cover:

* POST requests
* PUT requests
* DELETE requests
* Databases
* Prisma
* MySQL
* Authentication
* Form submission to APIs

Those topics come in later steps of the roadmap. 

---

## Next Lesson

Once you're comfortable with these concepts, we'll continue to **Step 32 (Hands-on)** by creating your **first `GET` API route**, sending a JSON response, and testing it in the browser and other tools. We'll still stay within the scope of **GET** before moving on to **Step 33 (POST)**, exactly as defined in your roadmap. 
