**Phase 3 — App Router**

# Step 3 — Dynamic Routes

## Today's Goal

By the end of this lesson, you'll be able to answer:

* What is a dynamic route?
* Why do we need dynamic routes?
* What is `[id]`?
* How does Next.js know which URL was requested?
* When should I use a dynamic route instead of creating many folders?

That's all.

---

## The Problem

Imagine you're building an e-commerce website.

You have these products:

* Laptop
* Mobile
* Monitor
* Keyboard
* Mouse

Based on what you've learned so far, you might think you need this structure:

```text
app/
└── products/
    ├── laptop/
    │   └── page.tsx
    ├── mobile/
    │   └── page.tsx
    ├── monitor/
    │   └── page.tsx
    ├── keyboard/
    │   └── page.tsx
    └── mouse/
        └── page.tsx
```

This works.

But imagine an online store with **50,000 products**.

Would you create **50,000 folders**?

❌ Of course not.

There has to be a better way.

---

## The Solution

Instead of creating one folder for every product, Next.js lets you create **one dynamic folder**.

```text
app/
└── products/
    └── [id]/
        └── page.tsx
```

Notice the square brackets:

```text
[id]
```

The brackets tell Next.js:

> "This part of the URL can be anything."

---

## What Does `[id]` Mean?

**Suppose someone visits:**

```text
/products/laptop
```

Next.js thinks:

```text
products
        ↓
[id]
```

Here:

```text
id = "laptop"
```

#

**Now someone visits:**

```text
/products/mobile
```

Next.js says:

```text
id = "mobile"
```

#

**Someone else visits:**

```text
/products/monitor
```

Now:

```text
id = "monitor"
```

The same page handles every URL.

---

## Visualizing It

Think of `[id]` as a placeholder.

```text
/products/______
```

The blank can be filled with:

```text
laptop

mobile

keyboard

mouse

monitor

anything...
```

---

## One Folder, Many URLs

This folder:

```text
products/
└── [id]/
    └── page.tsx
```

can respond to:

```text
/products/laptop
```

```text
/products/mobile
```

```text
/products/keyboard
```

```text
/products/monitor
```

```text
/products/mouse
```

All using **one** `page.tsx`.

---

## Real-World Examples

### Example 1 — Blog

Instead of:

```text
/blog/nextjs

/blog/react

/blog/typescript
```

You create:

```text
blog/
└── [slug]/
```

Possible URLs:

```text
/blog/nextjs
```

```text
/blog/react
```

```text
/blog/typescript
```

#

### Example 2 — Users

Instead of

```text
/users/john

/users/alice

/users/bob
```

Create:

```text
users/
└── [username]/
```

#

### Example 3 — Orders

Instead of

```text
/orders/1001

/orders/1002

/orders/1003
```

Use:

```text
orders/
└── [orderId]/
```

---

## Why Is It Called "Dynamic"?

Because the value changes.

Today:

```text
/products/laptop
```

Tomorrow:

```text
/products/mouse
```

Next week:

```text
/products/12345
```

The URL isn't fixed—it changes depending on what the user requests.

---

## The Folder Name Isn't Special

Many beginners think they must use:

```text
[id]
```

Actually, you can choose any meaningful name.

For example:

```text
[productId]
```

or

```text
[slug]
```

or

```text
[username]
```

or

```text
[orderId]
```

Choose a name that describes the value you're expecting.

---

## For a catch-all dynamic route, you have two options:

Let me clarify the folder structure for the App Router:

### Option 1: Just the `[id]` folder.
```
products/
└── [id]/
    └── page.tsx
```
This handles:
- `/products/laptop`
- `/products/mobile`
- `/products/keyboard`
- etc.

### Option 2: With a `page.tsx` in the products folder too
```
products/
├── page.tsx          ← Optional: handles /products
└── [id]/
    └── page.tsx      ← Handles /products/laptop, /products/mobile, etc.
```

#

### Which one do you need?

**Option 1** is enough if you ONLY want:
- `/products/laptop`
- `/products/mobile`
- etc.

**Option 2** adds support for:
- `/products` (the index page showing all products)

### Example code for both:

**`products/page.tsx` (if you want a listing page):**

```tsx
export default function ProductsPage() {
  return (
    <div>
      <h1>All Products</h1>
      <ul>
        <li><a href="/products/laptop">Laptop</a></li>
        <li><a href="/products/mobile">Mobile</a></li>
        {/* etc */}
      </ul>
    </div>
  );
}
```

**`products/[id]/page.tsx`:**
```tsx
export default function ProductPage({ params }: { params: { id: string } }) {
  return (
    <div>
      <h1>Product: {params.id}</h1>
    </div>
  );
}
```

So yes, you **can** have a `page.tsx` in the `products` folder if you want to handle `/products` route. 

Otherwise, just the `[id]/page.tsx` is sufficient!


---

## What Happens Internally?

Suppose the user visits:

```text
/products/laptop
```

Next.js works like this:

```text
Browser
      │
      ▼
/products/laptop
      │
      ▼
products/
      │
      ▼
[id]
      │
      ▼
page.tsx
```

It recognizes that `"laptop"` matches the dynamic segment and passes that value to your page.

Later, we'll learn how to read that value inside `page.tsx`. For today, it's enough to understand that the value is available to your code.

---

## Django Comparison

In Django, you might write:

```python
path("products/<int:id>/", views.product_detail)
```

or

```python
path("blog/<slug:slug>/", views.blog_detail)
```

Notice the similarity.

Django uses angle brackets:

```text
<int:id>
```

Next.js uses square brackets:

```text
[id]
```

Both represent a variable part of the URL.

---

## Static Route vs Dynamic Route

| Static Route         | Dynamic Route                  |
| -------------------- | ------------------------------ |
| `/about`             | `/products/[id]`               |
| URL never changes    | URL changes based on the value |
| One page for one URL | One page for many URLs         |
| Fixed folder name    | Folder name inside `[]`        |

---

## Rules to Remember

- Use a dynamic route when one page should handle many similar URLs.
- Put the folder name inside square brackets.
- The name inside the brackets is your choice.
- One `page.tsx` can serve thousands of URLs.

---

## Mini Exercise

### Question 1

Which folder structure can handle both:

```text
/products/laptop
```

and

```text
/products/mobile
```

A)

```text
products/
├── laptop/
└── mobile/
```

B)

```text
products/
└── [id]/
```

#

### Question 2

If you want URLs like:

```text
/users/alice
/users/bob
/users/charlie
```

What would you name the dynamic folder?

#

### Question 3

Is this a **static** or **dynamic** route?

```text
/blog/[slug]
```

---

## Lesson Summary

Today you learned the core idea behind dynamic routing:

> **A folder wrapped in square brackets (`[]`) acts as a placeholder for a changing part of the URL.**

This lets one page respond to many URLs, which is essential for things like product pages, blog posts, user profiles, and order details.

---

## Next Lesson (Step 4)

Next we'll learn **Layouts (`layout.tsx`)**.

So far, every page stands alone. In the next lesson, you'll discover how Next.js lets multiple pages share common UI—such as a navigation bar, sidebar, or footer—without duplicating the same code in every `page.tsx`. This is one of the most important concepts in the App Router and builds directly on the routing concepts you've already learned.
