**Phase 3 — App Router**

# Step 2 — Nested Routes

## Today's Goal

By the end of this lesson, you'll be able to answer:

* What is a nested route?
* Why do we use nested routes?
* How does Next.js create nested URLs?
* How do folders inside folders become URLs?

That's it.

---

## What is a Nested Route?

First, think about a real website.

Imagine an online shopping website.

Its URLs might look like:

```text
/
```

```text
/products
```

```text
/products/laptop
```

```text
/products/mobile
```

Notice something.

Both **laptop** and **mobile** belong to **products**.

Just like folders on your computer.

```
Products
│
├── Laptop
│
└── Mobile
```

A nested route works exactly like this.

---

## Think in Terms of Folders

Suppose your project looks like this:

```text
src/
└── app/
    ├── page.tsx
    └── products/
        └── page.tsx
```

What URLs exist?

```
/
```

and

```
/products
```

Why?

Because the **products** folder becomes:

```
/products
```

---

## Going One Level Deeper

Now suppose you create another folder.

```text
src/
└── app/
    ├── page.tsx
    └── products/
        ├── page.tsx
        └── laptop/
            └── page.tsx
```

Now your URLs become

```
/
```

```
/products
```

```
/products/laptop
```

Notice the pattern.

```
products
        ↓
products/laptop
```

The URL follows the folder structure.

---

## Another Example

Suppose you create:

```text
app/
└── products/
    ├── page.tsx
    ├── laptop/
    │     └── page.tsx
    ├── mobile/
    │     └── page.tsx
    └── monitor/
          └── page.tsx
```

Available URLs

```
/products
```

```
/products/laptop
```

```
/products/mobile
```

```
/products/monitor
```

Again...

No routing configuration.

No `urls.py`.

Just folders.

---

## Visualizing the Flow

Think of the folders as a tree.

```text
app
│
└── products
     │
     ├── laptop
     │
     ├── mobile
     │
     └── monitor
```

Next.js automatically understands this as

```text
/products

/products/laptop

/products/mobile

/products/monitor
```

---

## Comparison with Django

Suppose you wanted the same routes in Django.

You would probably write something like:

```python
path("products/", ...)
path("products/laptop/", ...)
path("products/mobile/", ...)
```

Every URL must be declared.

Next.js says:

> "Just create the folders."

---

## A Real-World Example

Imagine a company website.

You may have:

```text
/
```

Home page

#

```text
/services
```

All services

#

```text
/services/cloud
```

Cloud Services

#

```text
/services/network
```

Network Services

#

Your folder structure would be:

```text
app/
├── page.tsx
└── services/
    ├── page.tsx
    ├── cloud/
    │   └── page.tsx
    └── network/
        └── page.tsx
```

Everything stays organized because the URL structure matches the folder structure.

---

## The Golden Rule

Every new folder extends the URL.

For example:

```text
app/

products/

laptop/

gaming/
```

becomes

```
/products/laptop/gaming
```

You don't have to tell Next.js how to build this URL—it figures it out from the folders.

---

## Important Note

Having a folder **alone** is not enough.

For example:

```text
app/
└── products/
    └── laptop/
```

There is **no** `page.tsx` file.

Can you visit:

```
/products/laptop
```

❌ No.

A route must have a `page.tsx` to display content.

Without it, Next.js has nothing to render for that route.

---

## Mental Model

Instead of thinking:

```
URL
```

Think:

```
Folder
```

Every folder...

↓

creates

↓

part of the URL.

---

## Rules to Remember

✅ A folder inside another folder creates a nested URL.

✅ Every route needs a `page.tsx`.

✅ Folder hierarchy equals URL hierarchy.

✅ No routing configuration is required.

---

## Mini Exercise

### Question 1

If your folders are:

```text
app/
└── blog/
    └── page.tsx
```

What URL is created?

#

### Question 2

If your folders are:

```text
app/
└── products/
    └── laptop/
        └── page.tsx
```

What URL is created?

#

### Question 3

If your folders are:

```text
app/
└── company/
    ├── about/
    │   └── page.tsx
    └── careers/
        └── page.tsx
```

Which URLs are available?

---

## Lesson Summary

Today you learned one new concept:

> **Nested folders create nested URLs.**

This is one of the core ideas of the App Router. Once you understand that the URL hierarchy mirrors the folder hierarchy, creating organized routes becomes straightforward.

---

## Next Lesson (Step 3)

In the next lesson, we'll learn **Dynamic Routes**, which answer questions like:

```
How can one page show many different products?
```

Instead of creating:

```text
/products/laptop
/products/mobile
/products/monitor
/products/keyboard
```

you'll learn how a **single folder** can handle all of those URLs using a dynamic segment like:

```text
/products/[id]
```

This is where Next.js routing becomes much more powerful, but we'll tackle it one concept at a time.
