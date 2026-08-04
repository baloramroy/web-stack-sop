**Phase 8 — Forms**

# Step 1 — Create Forms (Next.js)

## Learning Objective

By the end of this lesson, you'll understand:

* What a form is
* Why forms exist
* The basic HTML elements of a form
* How forms fit into a Next.js application

**Today we are only creating the form.**

---

## What is a Form?

A form is simply a way for users to send information to your application.

Examples:

* Login page
* Registration page
* Contact page
* Search box
* Profile update
* Feedback form

Every one of these is a form.

---

## Real-Life Example

Imagine you're filling out a paper application at a bank.

The paper has boxes like:

```text
Name: ___________________

Email: __________________

Phone: _________________

[Submit]
```

A web form is exactly the same idea.

Instead of paper, it appears in the browser.

---

## Forms in Next.js

Next.js doesn't have a special "form system."

It uses normal HTML forms inside React components.

For example:

```tsx
export default function ContactPage() {
  return (
    <form>
      ...
    </form>
  );
}
```

Notice something important.

The `<form>` element is **HTML**, not Next.js.

Next.js simply renders it using React.

---

## The Main HTML Elements

A form usually contains:

```text
<form>

<input>

<label>

<button>

<textarea>

<select>

</form>
```

We'll learn them one by one.

---

## The `<form>` Element

Everything belongs inside:

```html
<form>

</form>
```

Think of it as a container.

Example:

```html
<form>
  ...
</form>
```

Without a `<form>`, the browser doesn't know these fields belong together.

---

## The `<input>` Element

This is where the user types information.

Example:

```html
<input type="text" />
```

Browser:

```text
____________________
```

---

Another example:

```html
<input type="email" />
```

Browser:

```text
Email

____________________
```

---

Password:

```html
<input type="password" />
```

Browser:

```text
*************
```

---

## The `<label>` Element

Labels describe an input.

Example:

```html
<label>Name</label>

<input type="text" />
```

Browser:

```text
Name

______________
```

Without labels, users don't know what to enter.

---

## The `<button>` Element

Buttons perform an action.

Example:

```html
<button>
    Submit
</button>
```

Browser:

```text
[ Submit ]
```

For forms, this button is typically used to submit the entered information.

---

## Your First Form

Create a new page.

```text
src/app/contact/page.tsx
```

Add the following code:

```tsx
export default function ContactPage() {
  return (
    <main>
      <h1>Contact Form</h1>

      <form>
        <label>Name</label>
        <br />
        <input type="text" />

        <br />
        <br />

        <label>Email</label>
        <br />
        <input type="email" />

        <br />
        <br />

        <button>Submit</button>
      </form>
    </main>
  );
}
```

Start your development server:

```bash
npm run dev
```

Visit:

```text
http://localhost:3000/contact
```

You should see something similar to:

```text
Contact Form

Name
_____________

Email
_____________

[ Submit ]
```

Congratulations!

You've created your first form in a Next.js application.

---

## How Does This Fit into Next.js?

Remember the flow we learned earlier in the roadmap:

```text
Browser
      │
      ▼
localhost:3000/contact
      │
      ▼
App Router
      │
      ▼
page.tsx
      │
      ▼
React Component
      │
      ▼
HTML
      │
      ▼
Browser
```

The `<form>` is simply part of the HTML that your React component returns.

Nothing special happens yet.

---

## What Happens When You Click "Submit"?

Right now...

**Nothing useful.**

Why?

Because we haven't told React what to do when the form is submitted.

That is exactly what we'll learn in **Step 30 — Handle Form Submission**.

---

## Common Beginner Mistakes

### 1. Thinking forms are a Next.js feature

They're not.

Forms are standard HTML elements that Next.js renders through React.

#

### 2. Forgetting the `<form>` tag

Wrong:

```html
<input type="text" />
<button>Submit</button>
```

Correct:

```html
<form>
  <input type="text" />
  <button>Submit</button>
</form>
```

#

### 3. Forgetting labels

Always tell users what each input is for.

```html
<label>Email</label>
<input type="email" />
```

---

## Step 1 Summary

Today you learned:

* ✅ What a form is.
* ✅ Why forms are used.
* ✅ The purpose of `<form>`, `<input>`, `<label>`, and `<button>`.
* ✅ How to create a simple form in a Next.js page.
* ✅ How that form fits into the Next.js rendering flow.

---

## Next Lesson

We'll continue with **Phase 8 – Step 2: Handle Form Submission**, where you'll learn:

* What happens when the user clicks **Submit**
* The `onSubmit` event
* `event.preventDefault()`
* Reading the user's input
* The complete submission flow in a Next.js application

This time, everything will be taught using **React and Next.js only**, staying consistent with your roadmap. 
