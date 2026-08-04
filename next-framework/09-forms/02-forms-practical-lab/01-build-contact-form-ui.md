**Phase 8 Practical Lab**

# Part 1 — Build the Contact Form UI

## Goal

Today we'll **only build the user interface**.

By the end of this lesson, you'll have a page that looks like this:

```text
------------------------------------

        Contact Us

Name
[________________________]

Email
[________________________]

Message
[________________________]
[                        ]
[                        ]

            [ Submit ]

------------------------------------
```

Notice something important.

The form **does nothing yet**.

That's intentional.

Today we're only building the UI.

---

## Before Writing Code

Let's think like a web developer.

If someone says:

> "Build a Contact Form"

What pieces do we need?

Let's list them.

```text
Title

↓

Form

↓

Name

↓

Email

↓

Message

↓

Submit Button
```

Everything belongs inside the form.

---

## Project Structure

We'll create a dedicated page.

```
src/
│
└── app/
    │
    └── contact/
        │
        └── page.tsx
```

Why?

Because of something you learned back in **Phase 3 (App Router)**.

Folders create routes.

```
contact/

↓

/contact
```

So visiting

```
http://localhost:3000/contact
```

will render:

```
page.tsx
```

---

## Step 1 — Create the Page

Inside:

```text
src/app/contact/page.tsx
```

write:

```tsx
export default function ContactPage() {
  return (
    <main>

    </main>
  );
}
```

Let's understand this.

#

### Why `export default`?

This tells Next.js:

> "This is the component for this page."

Every page in the App Router exports one default React component.

#

### Why `<main>`?

HTML provides semantic elements.

Some common ones are:

```text
<header>

<nav>

<main>

<footer>
```

`<main>` represents the primary content of the page.

Instead of writing:

```tsx
<div>

</div>
```

we'll use:

```tsx
<main>

</main>
```

because it better describes the content.

---

## Step 2 — Add a Heading

Inside `<main>`:

```tsx
<h1>Contact Us</h1>
```

Now your page becomes:

```tsx
export default function ContactPage() {
  return (
    <main>
      <h1>Contact Us</h1>
    </main>
  );
}
```

Open

```
http://localhost:3000/contact
```

You should see:

```
Contact Us
```

---

## Step 3 — Add the Form

Under the heading:

```tsx
<form>

</form>
```

Now:

```tsx
export default function ContactPage() {
  return (
    <main>
      <h1>Contact Us</h1>

      <form>

      </form>

    </main>
  );
}
```

Think of the form as a folder.

Everything related to user input belongs inside it.

---

## Step 4 — Name Field

Let's build the first field.

```tsx
<label htmlFor="name">
  Name
</label>

<input
  id="name"
  type="text"
/>
```

Notice something new.

```tsx
htmlFor
```

instead of

```html
for
```

Why?

Because in JSX, `for` is a reserved JavaScript keyword.

React uses:

```tsx
htmlFor
```

to generate HTML like:

```html
<label for="name">
```

#

### Why `id="name"`?

The label needs to know which input it belongs to.

```
Label

↓

htmlFor="name"

↓

Input

↓

id="name"
```

Now if you click the word **Name**, the text cursor automatically moves into the input.

That's better for usability and accessibility.

---

## Step 5 — Email Field

Exactly the same pattern.

```tsx
<label htmlFor="email">
  Email
</label>

<input
  id="email"
  type="email"
/>
```

Notice we changed:

```
text

↓

email
```

Using `type="email"` gives the browser more information about the expected input. For example, mobile devices often show an email-friendly keyboard.

---

## Step 6 — Message Field

For longer text we don't use:

```tsx
<input />
```

Instead we use:

```tsx
<textarea
  id="message"
></textarea>
```

with its label:

```tsx
<label htmlFor="message">
  Message
</label>
```

Why not an input?

Because an input is designed for a **single line**.

A message usually needs multiple lines.

---

## Step 7 — Submit Button

Finally:

```tsx
<button type="submit">
  Submit
</button>
```

Notice we explicitly wrote:

```tsx
type="submit"
```

Even though a `<button>` inside a form defaults to submit, writing it explicitly makes your code clearer and easier to understand.

---

## Complete Code

```tsx
export default function ContactPage() {
  return (
    <main>
      <h1>Contact Us</h1>

      <form>
        <label htmlFor="name">
          Name
        </label>

        <br />

        <input
          id="name"
          type="text"
        />

        <br />
        <br />

        <label htmlFor="email">
          Email
        </label>

        <br />

        <input
          id="email"
          type="email"
        />

        <br />
        <br />

        <label htmlFor="message">
          Message
        </label>

        <br />

        <textarea
          id="message"
        ></textarea>

        <br />
        <br />

        <button type="submit">
          Submit
        </button>
      </form>
    </main>
  );
}
```

---

## What Have We Built?

```
Browser
     │
     ▼
Contact Us

Name
[____________]

Email
[____________]

Message
[____________]

[ Submit ]
```

This is a **real HTML form** rendered by a React component inside a Next.js page.

---

## What Doesn't Work Yet?

If you click **Submit**:

* ❌ Nothing useful happens.
* ❌ We don't know what the user typed.
* ❌ We aren't storing any data.
* ❌ We aren't validating anything.

And that's perfectly fine.

We're building one layer at a time.

---

## Why Are We Doing It This Way?

Many tutorials jump straight to:

* `useState`
* `onChange`
* `onSubmit`
* Validation
* API calls

That makes it hard to understand what's happening.

Instead, we're building the feature in layers:

```
UI
   ↓
State
   ↓
Submission
   ↓
Validation
   ↓
API
```

Each layer adds one new concept while reusing the previous one.

---

## Lab Part 1 Summary

Today you built:

* ✅ A new `/contact` page.
* ✅ A semantic page using `<main>`.
* ✅ A `<form>` element.
* ✅ Labels connected to inputs using `htmlFor` and `id`.
* ✅ A text input.
* ✅ An email input.
* ✅ A textarea.
* ✅ A submit button.

You now have the **visual structure** of a contact form.

---

## Next Lab

In **Part 2**, we'll transform this static form into an interactive React form by introducing:

* `"use client"`
* `useState`
* Controlled inputs
* `value`
* `onChange`

By the end of Part 2, every keystroke the user types will be stored in React state, preparing us for submission and validation in the following parts.
