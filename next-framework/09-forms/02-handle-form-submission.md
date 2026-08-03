Perfect. We'll continue **exactly according to your Next.js roadmap**.

We have completed:

* ✅ Step 29 — Create Forms

Now we start:

# Phase 8 — Forms

# Step 30 — Handle Form Submission

## Learning Objective

By the end of this lesson, you'll understand:

* What happens when the user clicks **Submit**
* What the `onSubmit` event is
* Why we use `event.preventDefault()`
* How to read the user's input
* The complete form submission flow in Next.js

> **Today we are not validating the data.** Validation belongs to **Step 31**, exactly as defined in your roadmap. 

---

# What Happens When You Click Submit?

Let's start with a simple form.

```tsx
<form>
  <input type="text" />
  <button>Submit</button>
</form>
```

Suppose the user types:

```text
Name: John
```

Then clicks:

```text
[ Submit ]
```

What happens?

---

# The Browser's Default Behavior

By default, HTML forms tell the browser:

> "Submit this form."

The browser will send the form data and then **reload the page**.

The flow looks like this:

```text
User
 │
 ▼
Fill Form
 │
 ▼
Click Submit
 │
 ▼
Browser submits form
 │
 ▼
Page Reloads
```

This is normal HTML behavior.

---

# Why Is This a Problem?

Modern React and Next.js applications usually **don't want the page to reload**.

Instead, we want to:

* Validate the data
* Send it to an API
* Show a success message
* Update the UI

...all **without refreshing the page**.

That's why React gives us the `onSubmit` event.

---

# The `onSubmit` Event

Instead of letting the browser handle the form, we can handle it ourselves.

```tsx
<form onSubmit={handleSubmit}>
```

Think of it like this:

```text
User clicks Submit
        │
        ▼
React calls
handleSubmit()
```

Instead of:

```text
Browser reloads page
```

---

# Creating the Submit Function

Let's update our page.

```tsx
export default function ContactPage() {

  function handleSubmit() {
    console.log("Form submitted");
  }

  return (
    <main>
      <form onSubmit={handleSubmit}>
        <label>Name</label>
        <br />
        <input type="text" />

        <br />
        <br />

        <button>Submit</button>
      </form>
    </main>
  );
}
```

Now:

1. Open the page.
2. Open the browser's Developer Tools (**F12 → Console**).
3. Click **Submit**.

You'll briefly see:

```text
Form submitted
```

But then the page reloads.

Why?

Because we haven't stopped the browser's default behavior yet.

---

# The Event Object

When React calls `handleSubmit`, it passes an **event object**.

```tsx
function handleSubmit(event) {

}
```

Think of the event object as information about **what just happened**.

In this case:

```text
A form was submitted.
```

So now our function becomes:

```tsx
function handleSubmit(event) {
  console.log("Form submitted");
}
```

---

# What Is `event.preventDefault()`?

The event object has a method called:

```tsx
event.preventDefault()
```

Its job is simple:

> "Don't perform the browser's default action."

For a form, the browser's default action is:

```text
Submit form

↓

Reload page
```

When we call:

```tsx
event.preventDefault();
```

the flow changes to:

```text
Submit form

↓

Stay on the same page
```

---

# Updating the Function

```tsx
function handleSubmit(event) {
  event.preventDefault();

  console.log("Form submitted");
}
```

Now try again.

1. Refresh the page once.
2. Open the Console.
3. Click **Submit**.

You'll see:

```text
Form submitted
```

This time, **the page does not reload**.

Congratulations!

You've taken control of the form submission.

---

# Reading the User's Input

Right now, our input has no way to remember what the user typed.

Let's introduce React state.

First, import `useState`.

```tsx
"use client";

import { useState } from "react";
```

Create state for the name.

```tsx
const [name, setName] = useState("");
```

Now connect the input.

```tsx
<input
  type="text"
  value={name}
  onChange={(event) => setName(event.target.value)}
/>
```

Now the value in the input is stored in the `name` state.

---

# Accessing the Submitted Value

Update the submit function.

```tsx
function handleSubmit(event) {
  event.preventDefault();

  console.log(name);
}
```

Suppose the user types:

```text
John
```

Then clicks **Submit**.

The Console shows:

```text
John
```

The data is now available inside your React component.

---

# Complete Example

```tsx
"use client";

import { useState } from "react";

export default function ContactPage() {
  const [name, setName] = useState("");

  function handleSubmit(event) {
    event.preventDefault();

    console.log(name);
  }

  return (
    <main>
      <h1>Contact Form</h1>

      <form onSubmit={handleSubmit}>
        <label>Name</label>
        <br />

        <input
          type="text"
          value={name}
          onChange={(event) => setName(event.target.value)}
        />

        <br />
        <br />

        <button type="submit">Submit</button>
      </form>
    </main>
  );
}
```

---

# Understanding the Flow

Here's what happens from start to finish.

```text
User
 │
 ▼
Types "John"
 │
 ▼
onChange
 │
 ▼
setName("John")
 │
 ▼
React State
 │
 ▼
Clicks Submit
 │
 ▼
onSubmit
 │
 ▼
handleSubmit()
 │
 ▼
event.preventDefault()
 │
 ▼
console.log(name)
```

Notice that **nothing has been sent to a server yet**.

Everything happens inside the browser.

---

# Why Do We Use State?

Without state:

```text
Input

↓

Browser knows the value

↓

React does not
```

With state:

```text
Input

↓

React State

↓

React knows the value
```

React applications typically keep form values in state so your component can work with them.

---

# Common Beginner Mistakes

### 1. Forgetting `"use client"`

Since we're using `useState` and event handlers like `onSubmit`, this component must be a **Client Component**.

```tsx
"use client";
```

Without it, Next.js will show an error because Server Components cannot use browser event handlers.

---

### 2. Forgetting `event.preventDefault()`

Without:

```tsx
event.preventDefault();
```

the browser reloads the page after submission.

---

### 3. Forgetting `onChange`

If you write:

```tsx
<input value={name} />
```

but don't provide an `onChange` handler, the input becomes read-only because React controls its value but never updates it.

---

# Step 30 Summary

Today you learned:

* ✅ What happens when a form is submitted.
* ✅ The purpose of the `onSubmit` event.
* ✅ Why `event.preventDefault()` is important.
* ✅ How to store input values using `useState`.
* ✅ How to read those values when the form is submitted.
* ✅ The complete submission flow inside a Next.js application.

At this point, your form can:

* Display inputs.
* Accept user input.
* Handle the submit event.
* Access the entered data.

**What it cannot do yet** is check whether the data is valid (for example, ensuring the name isn't empty or the email is correctly formatted). That is exactly what we'll learn in **Step 31 — Validation**, completing Phase 8 of your roadmap. 
