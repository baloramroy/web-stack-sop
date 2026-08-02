**Phase 5 — Components**

## Step 2 — Component Folder Organization

> **Today's Goal:** Learn **where** components should live and **how to organize** them in a clean, scalable project.


---

## Learning Goal

By the end of this lesson, you should be able to answer:

* Why shouldn't all components be in one folder?
* Where should reusable components be stored?
* How should component files be named?
* How do developers organize components in real projects?
* What is a clean folder structure for a beginner?

---

## The Problem

Imagine you keep every component in a single folder.

```text
components/
├── Button.tsx
├── Navbar.tsx
├── Footer.tsx
├── Card.tsx
├── ProductCard.tsx
├── UserCard.tsx
├── Sidebar.tsx
├── Modal.tsx
├── SearchBar.tsx
├── Hero.tsx
├── Testimonial.tsx
├── PricingCard.tsx
├── ...
```

At first, this looks fine.

But after building a larger application, you may have:

* 50 components
* 100 components
* 200+ components

Finding the one you need becomes harder.

---

## Why Folder Organization Matters

Think about a real office.

Would you put:

* HR documents
* Finance documents
* Legal documents
* Contracts

all into one drawer?

Of course not.

You organize them into folders.

Software projects follow the same principle.

Good organization makes projects:

* Easier to understand
* Easier to maintain
* Easier for teams to work on

---

## Where Do Components Live?

A common beginner-friendly structure is:

```text
src/
│
├── app/
├── components/
└── public/
```

Here:

```text
components/
```

contains reusable UI components.

Examples:

```text
src/
├── app/
├── components/
│   ├── Navbar.tsx
│   ├── Footer.tsx
│   ├── Button.tsx
│   ├── Card.tsx
│   └── Sidebar.tsx
└── public/
```

This is a great starting point and is perfectly acceptable for many projects.

---

## Why Not Put Components Inside `app/`?

The `app/` folder has a different responsibility.

It is used for:

* Routes
* Pages
* Layouts
* Loading UI
* Error UI

Example:

```text
app/
├── page.tsx
├── layout.tsx
├── about/
│   └── page.tsx
└── contact/
    └── page.tsx
```

Notice that these files represent **pages and routing**, not reusable UI.

A reusable `Button` or `Navbar` doesn't define a route, so it usually doesn't belong here.

Keeping routing and reusable UI separate makes the project easier to understand.

---

## Naming Components

Component file names usually use **PascalCase**.

Examples:

```text
Button.tsx
Navbar.tsx
Footer.tsx
ProductCard.tsx
UserProfile.tsx
SearchBar.tsx
```

Avoid names like:

```text
button.tsx
navbar.tsx
my_component.tsx
component1.tsx
```

Using PascalCase makes components easy to recognize.

---

## One Component Per File

A good practice is:

```text
Button.tsx
```

contains:

* One `Button` component.

```text
Navbar.tsx
```

contains:

* One `Navbar` component.

This keeps files focused and easier to read.

---

## Beginner Folder Structure

For now, this is all you need:

```text
src/
│
├── app/
│   ├── page.tsx
│   ├── layout.tsx
│   └── about/
│       └── page.tsx
│
├── components/
│   ├── Navbar.tsx
│   ├── Footer.tsx
│   ├── Button.tsx
│   └── Card.tsx
│
├── public/
│
├── styles/      (optional later)
│
└── lib/         (we'll learn this much later)
```

Don't worry about `styles/` or `lib/` yet—they're included only so you know they exist.

---

## How Pages Use Components

Think of the relationship like this:

```text
Home Page
│
├── Navbar
├── Hero
├── ProductCard
├── ProductCard
├── ProductCard
└── Footer
```

The page is responsible for **assembling** the UI.

The components are responsible for **rendering** each piece of that UI.

---

## Real-World Example

Imagine you're building an online shop.

You might have:

```text
components/
├── Navbar.tsx
├── Footer.tsx
├── ProductCard.tsx
├── ShoppingCart.tsx
├── SearchBar.tsx
├── CategoryMenu.tsx
└── Button.tsx
```

Then your home page might use them like this:

```text
Home Page
│
├── Navbar
├── SearchBar
├── CategoryMenu
├── ProductCard
├── ProductCard
├── ProductCard
└── Footer
```

The page doesn't need to know how each component is built. It simply places them where they belong.

---

## Beginner Mistakes to Avoid

❌ Putting every piece of code into `page.tsx`.

❌ Creating one giant component with hundreds of lines.

❌ Naming files inconsistently.

❌ Mixing routing files and reusable UI files without a clear reason.

---

## Best Practices (For Now)

* Keep reusable UI in `src/components/`.
* Use **PascalCase** for component names.
* Keep one main component per file.
* Let pages assemble components rather than containing all the UI themselves.

As you become more experienced, you'll learn more advanced organization patterns, but this structure is an excellent foundation.

---

## Mini Exercise (No Coding Yet)

Look at the following items and decide where they belong.

| Item                    | `app/` or `components/`? | Why? |
| ----------------------- | ------------------------ | ---- |
| `page.tsx` for `/about` | ?                        | ?    |
| `Navbar.tsx`            | ?                        | ?    |
| `Footer.tsx`            | ?                        | ?    |
| `layout.tsx`            | ?                        | ?    |
| `ProductCard.tsx`       | ?                        | ?    |
| `Button.tsx`            | ?                        | ?    |

Try to answer based on what you've learned today.

---

## Lesson Summary

Today we learned:

* ✅ Why folder organization is important.
* ✅ The purpose of the `components/` folder.
* ✅ Why routing files belong in `app/`.
* ✅ Why components should use PascalCase.
* ✅ Why one component per file is a good practice.
* ✅ A clean folder structure suitable for beginners.

---

## Completed So Far

* ✅ Step 1 — Create Reusable UI Components
* ✅ Step 2 — Component Folder Organization

**Next Lesson (Phase 6, Step 1):** **Understanding Server Components**.

This is one of the most important concepts in modern Next.js, so we'll take it slowly and build a strong mental model before writing code.
