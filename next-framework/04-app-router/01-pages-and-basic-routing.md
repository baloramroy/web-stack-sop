**Phase 3 — App Router**

# Step 1 — Pages & Basic Routing

## Today's Goal

By the end of this lesson, you should be able to answer:

* What is the App Router?
* How does Next.js create pages?
* Why do folders become URLs?
* What is `page.tsx`?
* How do I create a new page?

That's all. Nothing more today.

---

## Before We Start

Think about how Django works.

In Django, if you want an **About** page, you write something like:

```
Browser
    │
    ▼
urls.py
    │
    ▼
views.py
    │
    ▼
template
```

The URL exists because **you explicitly define it** in `urls.py`.

For example:

```python
path("about/", views.about)
```

So Django asks:

> **"What URL did the developer configure?"**

---

## Next.js Thinks Differently

Next.js doesn't ask:

> "Did you configure the URL?"

Instead, it asks:

> **"What folders exist?"**

That is one of the biggest differences between Django and Next.js.

---

## The Golden Rule

> **Every folder containing a `page.tsx` file becomes a route (URL).**

Remember this sentence. You'll use it every day when working with Next.js.

---

## Example 1

Suppose your project looks like this:

```text
src/
└── app/
    └── page.tsx
```

Your URL will be:

```
http://localhost:3000/
```

Why?

Because the `page.tsx` file is directly inside the `app` folder, which represents the root (`/`) route.

---

## Example 2

Now create this structure:

```text
src/
└── app/
    ├── page.tsx
    └── about/
        └── page.tsx
```

What URLs are available?

```
/
```

and

```
/about
```

Notice that we never wrote a routing configuration file.

The folder name (`about`) automatically became part of the URL.

---

## Example 3

Create another folder:

```text
src/
└── app/
    ├── page.tsx
    ├── about/
    │   └── page.tsx
    └── contact/
        └── page.tsx
```

Available URLs:

```
/
```

```
/about
```

```
/contact
```

Again, no routing configuration is needed.

---

## Visualizing the Routing

Think of your folders as a map.

```text
app
│
├── page.tsx
│
├── about
│      │
│      └── page.tsx
│
└── contact
       │
       └── page.tsx
```

becomes:

```text
/

↓

about/

↓

contact/
```

A useful way to remember it is:

```text
Folder Name
      ↓
Becomes
      ↓
URL Path
```

---

## What Does `page.tsx` Do?

Every route needs a page to display.

For example:

```
/about
```

needs something to show in the browser.

That "something" is `page.tsx`.

If `page.tsx` doesn't exist, there is no page to render for that route.

---

## Your First Page

Suppose `src/app/about/page.tsx` contains:

```tsx
export default function AboutPage() {
  return <h1>About Us</h1>;
}
```

When you visit:

```
http://localhost:3000/about
```

You'll see:

```text
About Us
```

The function name (`AboutPage`) can be anything meaningful. What matters is that it is the **default export**, because Next.js looks for the default exported component in `page.tsx`.

---

## Comparing Django and Next.js

| Django                     | Next.js                                    |
| -------------------------- | ------------------------------------------ |
| Define routes in `urls.py` | Create folders                             |
| Route points to a view     | Folder contains `page.tsx`                 |
| View returns HTML/template | `page.tsx` returns a React component       |
| URL is manually configured | URL is generated from the folder structure |

---

## Rules to Remember

✅ Every route must have a `page.tsx` file.

✅ Folder names become URL paths.

✅ The `app` folder is the starting point for routing.

✅ No `urls.py` is required.

---

## Mini Exercise

Without creating the project yet, try to answer these questions.

### Question 1

If your folder structure is:

```text
app/
├── page.tsx
└── services/
    └── page.tsx
```

What URLs will be available?

#

### Question 2

If your folder structure is:

```text
app/
├── page.tsx
├── blog/
│   └── page.tsx
└── contact/
    └── page.tsx
```

What URLs can users visit?

#

### Question 3

Which file actually displays the content of a page?

* A. `layout.tsx`
* B. `page.tsx`
* C. `package.json`
* D. `globals.css`

---

## Lesson Summary

Today you learned only one concept:

> **Folders create routes, and `page.tsx` defines what is displayed for each route.**

Everything else in the App Router—nested routes, dynamic routes, layouts, and navigation—builds on this idea.

---

## Next Lesson (Step 2)

Once you're comfortable with today's lesson, we'll move on to **Nested Routes**, where you'll learn how to create URLs like:

```text
/products
/products/laptop
/products/mobile
```

using folders inside folders. We won't cover dynamic routes or layouts until after you've mastered this basic routing concept.
