**Phase 4 — Styling**

## Step 3 — Tailwind CSS


## Lesson Goal

By the end of this lesson, you'll be able to answer:

* What is Tailwind CSS?
* Why do modern Next.js projects use Tailwind CSS?
* How is Tailwind different from normal CSS?
* What are utility classes?
* When should we use Tailwind?
* How does Tailwind work behind the scenes?

**Today's goal is understanding the concept.**

We will **not** memorize lots of Tailwind classes today.

---

## Before We Start

You may have noticed something in your project.

Open:

```text
src/app/globals.css
```

You'll probably see:

```css
@import "tailwindcss";
```

You might have wondered:

> "Why is Tailwind already here?"

The answer is simple.

When you created your Next.js project, you answered:

```text
Would you like to use Tailwind CSS?

Yes
```

So Next.js installed and configured Tailwind automatically.

---

## What is Tailwind CSS?

Tailwind CSS is a **CSS framework**.

But it is very different from frameworks like Bootstrap.

Instead of giving you ready-made components,

Tailwind gives you **small utility classes** that you combine to build your own designs.

---

## Traditional CSS

Normally, you write CSS first.

Example:

```css
.button {
    background: blue;
    color: white;
    padding: 12px;
    border-radius: 8px;
}
```

Then in HTML:

```html
<button class="button">
    Save
</button>
```

Two files are involved:

```text
Button.tsx

↓

Button.module.css
```

---

## Tailwind CSS

With Tailwind,

you usually don't create a CSS class first.

Instead, you write utility classes directly in your component.

Example:

```tsx
<button className="bg-blue-500 text-white p-3 rounded">
    Save
</button>
```

Everything is written in one place.

No separate CSS file is needed for simple styling.

---

## Real-World Analogy

Imagine you're building with LEGO.

### Traditional CSS

You build a complete chair.

```
Chair
```

Then you use it.

#

### Tailwind

Instead, you receive small LEGO blocks.

```
Blue block

+

Round block

+

Padding block

+

Shadow block
```

You combine them yourself.

Tailwind works exactly like that.

---

## What is a Utility Class?

A utility class does **one thing only**.

Examples:

```text
bg-blue-500
```

Means:

```
Background color
```

#

```text
text-white
```

Means:

```
Text color
```

#

```text
p-4
```

Means:

```
Padding
```

#

```text
rounded
```

Means:

```
Rounded corners
```

#

Each class has **one responsibility**.

You combine many small classes to create the final design.

---

## Example

Traditional CSS

```css
.card {
    background: white;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 2px 8px gray;
}
```

---

Tailwind

```tsx
<div className="bg-white p-5 rounded-xl shadow">
```

Both produce the same result.

The difference is **where** the styles are defined.

---

## Why Do Developers Like Tailwind?

Imagine you're working on a project with hundreds of components.

Traditional CSS often creates problems like:

```
Where is this CSS class?

Which file contains it?

Is it safe to delete?

Will changing it affect another page?
```

With Tailwind,

the styles are written where the component lives.

You don't have to search for another file.

---

## Does Tailwind Replace CSS?

`No.`

This is a common misunderstanding.

Tailwind is still CSS.

It simply provides many predefined utility classes.

You can still write:

```css
.button {
    ...
}
```

whenever you need to.

Many projects use:

* Tailwind
* CSS Modules
* Global CSS

together.

---

## Global CSS vs CSS Modules vs Tailwind

### Global CSS

Best for:

* Fonts
* Body styles
* CSS reset
* Variables

Example:

```css
body {
    margin: 0;
}
```

#

### CSS Modules

Best for:

* Large custom component styles

Example:

```text
Button.module.css
```

#

### Tailwind

Best for:

* Layout
* Spacing
* Flexbox
* Grid
* Colors
* Responsive design
* Most day-to-day component styling


Modern Next.js projects commonly use **all three**, each for the job it's best suited to.

---

## How Does Tailwind Work?

Suppose you write:

```tsx
className="bg-blue-500 text-white"
```

Tailwind scans your project.

It finds:

```text
bg-blue-500

text-white
```

Then it generates only the CSS needed for those classes.

You don't get thousands of unused styles.

---

## Request Flow

Here's what happens:

```text
Developer

↓

Writes Tailwind classes

↓

Tailwind scans project

↓

Generates required CSS

↓

Next.js bundles CSS

↓

Browser receives CSS

↓

Page is styled
```

---

## Is Tailwind Faster?

In terms of development:

Yes.

You write less CSS.

You switch between files less often.

#

In terms of performance:

Also yes.

Tailwind generates only the CSS your project actually uses.

This helps keep the final CSS bundle smaller.

---

## Common Utility Categories

You don't need to memorize these yet, but it's useful to know the categories.

| Category       | Examples                                 |
| -------------- | ---------------------------------------- |
| Colors         | `bg-blue-500`, `text-red-500`            |
| Spacing        | `p-4`, `m-6`                             |
| Typography     | `text-xl`, `font-bold`                   |
| Borders        | `border`, `rounded-lg`                   |
| Flexbox        | `flex`, `justify-center`, `items-center` |
| Grid           | `grid`, `grid-cols-3`                    |
| Width & Height | `w-full`, `h-screen`                     |
| Shadows        | `shadow`, `shadow-lg`                    |

We'll explore these gradually in future lessons and projects.

---

## Should Beginners Learn Tailwind?

Yes.

But not by memorizing every class.

Instead:

1. Learn what each utility does.
2. Use the documentation when needed.
3. Over time, common classes become familiar through practice.

Even experienced developers look up Tailwind classes regularly.

---

## Today's Key Takeaways

* Tailwind CSS is a utility-first CSS framework.
* A utility class performs one specific styling task.
* Tailwind lets you style components directly in `className`.
* Tailwind complements Global CSS and CSS Modules rather than replacing them.
* Next.js scans your code and generates only the CSS you actually use.

---

## Practice (20–30 Minutes)

Open your default `page.tsx`.

Without creating any CSS files, try making a simple page that includes:

* A centered heading
* A paragraph below it
* A button

Use Tailwind utility classes to:

* Increase the heading size
* Make the heading bold
* Add spacing between elements
* Give the button a background color
* Add padding to the button
* Round the button's corners

Don't worry about making it look perfect. The goal is to get comfortable reading and using utility classes.

---

## Before We Move to Phase 5

Make sure you can answer these questions:

1. What is Tailwind CSS?
2. What is a utility class?
3. How is Tailwind different from writing CSS Modules?
4. Can Tailwind, Global CSS, and CSS Modules be used together?
5. Why do many Next.js projects choose Tailwind CSS?

Once you're comfortable with those answers, we'll begin **Phase 5 — Components**, starting with **Creating Reusable Components**, where we'll start organizing our application into reusable building blocks instead of putting everything in `page.tsx`.
