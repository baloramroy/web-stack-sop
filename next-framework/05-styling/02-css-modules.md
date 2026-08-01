**Phase 4 — Styling**

# Step 17 — CSS Modules

## Lesson Goal

By the end of this lesson, you'll be able to answer:

* What is a CSS Module?
* Why do we need CSS Modules?
* How are CSS Modules different from Global CSS?
* How do we create and use a CSS Module in Next.js?
* When should we use a CSS Module instead of `globals.css`?

---

## Recap of the Previous Lesson

In Step 16, we learned:

```
globals.css
```

which applies styles to the **entire application**.

Example:

```css
body {
    font-family: Arial, sans-serif;
}
```

Every page uses this style because `globals.css` is imported into `layout.tsx`.

Now let's solve a different problem.

---

## The Problem

Imagine you have two buttons.

Home page:

```text
Save
```

Profile page:

```text
Delete
```

You write this in `globals.css`:

```css
button {
    background: green;
    color: white;
}
```

What happens?

Both buttons become green.

```
Home
┌──────────────┐
│ Save (Green) │
└──────────────┘

Profile
┌────────────────┐
│ Delete (Green) │
└────────────────┘
```

But maybe you wanted:

```
Save → Green

Delete → Red
```

Global CSS cannot easily separate those styles.

---

## The Solution: CSS Modules

A CSS Module is a CSS file whose styles belong **only to one component**.

Think of it like giving each component its own private stylesheet.

Instead of one huge style file:

```text
globals.css
```

you have:

```text
Button.module.css
```

Only the `Button` component can use it.

---

## Real-World Analogy

Imagine an apartment building.

### Global CSS

Building-wide rules:

* White walls
* Same hallway lights
* Same elevators

Everyone shares them.

#

### CSS Modules

Each apartment can choose:

* Wall color
* Furniture
* Curtains
* Decorations

Changing Apartment 5 doesn't affect Apartment 6.

That's exactly how CSS Modules work.

---

# File Structure

Suppose you have:

```text
src/
└── app/
    ├── page.tsx
    ├── globals.css
    └── components/
        ├── Button.tsx
        └── Button.module.css
```

Notice the naming convention:

```
Button.module.css
```

The `.module.css` part is important.

Next.js recognizes it as a CSS Module.

---

## Creating a CSS Module

Example:

```css
.button {
    background: green;
    color: white;
    padding: 12px;
}
```

This class is **not global**.

It belongs only to the component that imports it.

---

## Importing a CSS Module

Inside your component:

```tsx
import styles from "./Button.module.css";
```

Notice something new:

```tsx
styles
```

Instead of importing the file only for its side effects (like `globals.css`), you're importing an object that contains your class names.

---

## Using the Styles

Instead of:

```tsx
<button className="button">
```

you write:

```tsx
<button className={styles.button}>
```

Why?

Because Next.js maps your class names to unique names behind the scenes.

---

## What Next.js Does Internally

You write:

```css
.button
```

Next.js may generate something like:

```css
.button_a8X93
```

or

```css
.button__2PqK1
```

Then your HTML becomes something like:

```html
<button class="button_a8X93">
```

This happens automatically.

---

## Why Is This Useful?

Imagine two different components.

### Login Button

```css
.button {
    background: blue;
}
```

### Dashboard Button

```css
.button {
    background: red;
}
```

Normally, CSS would see both as:

```
.button
```

and one style could overwrite the other.

With CSS Modules, Next.js generates unique names, so both components keep their own styles.

---

## Global CSS vs CSS Modules

| Global CSS                    | CSS Modules                    |
| ----------------------------- | ------------------------------ |
| Affects the whole application | Affects only one component     |
| Imported in `layout.tsx`      | Imported inside a component    |
| Good for fonts, body, resets  | Good for buttons, cards, forms |
| Shared by everyone            | Private to one component       |

---

## When Should You Use Each?

Use **Global CSS** for:

* Application font
* Background color
* CSS reset
* Variables
* Common utility styles

Use **CSS Modules** for:

* Button styles
* Card styles
* Navbar styles
* Footer styles
* Form styles
* Sidebar styles

A good rule of thumb:

> If the style belongs to a specific component, put it in a CSS Module.

---

## Request Flow

Let's see where CSS Modules fit.

```
Browser
      │
      ▼
page.tsx
      │
      ▼
Button.tsx
      │
      ▼
Button.module.css
      │
      ▼
Next.js generates unique class names
      │
      ▼
Styled HTML
      │
      ▼
Browser
```

Unlike `globals.css`, the CSS Module is loaded only when its component is used.

---

## Small Example

Imagine you create a button component.

**Button.tsx**

```tsx
import styles from "./Button.module.css";

export default function Button() {
    return (
        <button className={styles.button}>
            Save
        </button>
    );
}
```

**Button.module.css**

```css
.button {
    background: green;
    color: white;
    padding: 10px 20px;
    border-radius: 6px;
}
```

Result:

```
┌──────────────┐
│ Save         │
└──────────────┘
```

Only this button gets those styles.

---

## Best Practices

- Keep one CSS Module per component when the component has its own styles.
- Use meaningful class names like:

    ```css
    .button
    .card
    .title
    .container
    ```

- Don't worry if multiple components use `.button` as a class name. CSS Modules keep them isolated.
- Don't put component-specific styles in `globals.css`.
- Don't create one giant CSS Module for your whole application.

---

## Today's Key Takeaways

* A CSS Module is a stylesheet that belongs to a single component.
* CSS Modules prevent style conflicts by generating unique class names.
* CSS Modules are imported into components, not into `layout.tsx`.
* Use `className={styles.className}` to apply module styles.
* Use Global CSS for application-wide styles and CSS Modules for component-specific styles.

---

## Practice (20–30 Minutes)

Create a simple button component and style it using a CSS Module.

1. Create a `components` folder inside `src/app`.
2. Create:

   * `Button.tsx`
   * `Button.module.css`
3. Add a `.button` class to `Button.module.css`.
4. Import the module in `Button.tsx` using:

   ```tsx
   import styles from "./Button.module.css";
   ```
5. Apply the class with:

   ```tsx
   className={styles.button}
   ```
6. Import the `Button` component into `page.tsx` and verify that it appears with your custom styles.
7. Try changing the button's background color and border radius to see the changes update automatically.
