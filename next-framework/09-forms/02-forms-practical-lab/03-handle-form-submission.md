**Phase 8 Practical Lab**

# Part 3 — Handle Form Submission

So far we've built:

* ✅ Part 1 — Form UI
* ✅ Part 2 — React State (Controlled Components)

Today we'll make the form actually **submit**.

---

## Learning Objective

By the end of this lesson, you'll understand:

* How React handles form submission
* What the `onSubmit` event is
* What the `event` object contains
* Why `event.preventDefault()` is important
* How to access all the entered values when the user submits the form

> **Today we are not validating the data and we are not sending it to an API.**
>
> Our only goal is to successfully receive the submitted data inside our React component.

---

## Before Writing Any Code

Let's think about what should happen.

The user fills in:

```text
Name: John

Email: john@gmail.com

Message: Hello, I need some help.
```

Then clicks:

```text
[ Submit ]
```

Where should this information go?

In our application, we want it to reach a function that we control.

```text
User

↓

Submit Button

↓

handleSubmit()

↓

React Component
```

That function will decide what happens next.

---

## Step 1 — The Browser's Default Behavior

Without React, an HTML form behaves like this:

```html
<form>

</form>
```

When the user clicks **Submit**:

```text
User

↓

Click Submit

↓

Browser Submits Form

↓

Page Reloads
```

You may have already noticed this behavior on many traditional websites.

---

## Why Is This a Problem?

Modern React applications don't usually want to reload the page.

Instead, we want to:

* Read the entered values
* Validate them
* Send them to an API
* Show success or error messages

...all while staying on the same page.

So we need to stop the browser from doing its default job.

---

## Step 2 — Create a Submit Function

Inside your component, create a new function.

```tsx
function handleSubmit(event: React.FormEvent<HTMLFormElement>) {

}
```

Let's understand this line.

#

### Why is it called `handleSubmit`?

The name isn't special.

These are all valid:

```tsx
function submitForm() {}
```

```tsx
function onSubmit() {}
```

```tsx
function myFunction() {}
```

We use **`handleSubmit`** because it's a common React naming convention.

It clearly tells us:

> "This function handles the form submission."

---

## Step 3 — The Event Object

Notice the parameter:

```tsx
event
```

When the form is submitted, React automatically passes an object describing what happened.

```text
User Clicks Submit

↓

React

↓

event
```

This object contains information about the submission.

For today's lesson, we only need one method from it.

---

## Step 4 — Prevent the Default Behavior

Inside the function, write:

```tsx
function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
  event.preventDefault();
}
```

This is one of the most common lines you'll write when working with forms.

It tells the browser:

> "Don't perform your default form submission."

So instead of:

```text
Submit

↓

Reload Page
```

We now have:

```text
Submit

↓

Stay on Current Page
```

---

## Step 5 — Connect the Form

Right now your form looks like this:

```tsx
<form>
```

Update it to:

```tsx
<form onSubmit={handleSubmit}>
```

Now the connection is complete.

```text
<form>

↓

onSubmit

↓

handleSubmit()
```

Whenever the user submits the form, React calls your function.

---

## Step 6 — Display the Submitted Data

Remember our state variables?

```tsx
const [name, setName] = useState("");
const [email, setEmail] = useState("");
const [message, setMessage] = useState("");
```

These always contain the latest values.

So inside `handleSubmit()`, write:

```tsx
function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
  event.preventDefault();

  console.log("Submitted Data");

  console.log("Name:", name);
  console.log("Email:", email);
  console.log("Message:", message);
}
```

---

## What Happens Now?

Suppose the user enters:

```text
Name: John

Email: john@gmail.com

Message: Hello
```

Then clicks **Submit**.

Your browser console will show:

```text
Submitted Data

Name: John

Email: john@gmail.com

Message: Hello
```

Congratulations!

You've successfully received all the user's input inside your React component.

---

## Complete Code

```tsx
"use client";

import { useState } from "react";

export default function ContactPage() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [message, setMessage] = useState("");

  function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
    event.preventDefault();

    console.log("Submitted Data");

    console.log("Name:", name);
    console.log("Email:", email);
    console.log("Message:", message);
  }

  return (
    <main>
      <h1>Contact Us</h1>

      <form onSubmit={handleSubmit}>
        <label htmlFor="name">Name</label>
        <br />
        <input
          id="name"
          type="text"
          value={name}
          onChange={(event) => setName(event.target.value)}
        />

        <br />
        <br />

        <label htmlFor="email">Email</label>
        <br />
        <input
          id="email"
          type="email"
          value={email}
          onChange={(event) => setEmail(event.target.value)}
        />

        <br />
        <br />

        <label htmlFor="message">Message</label>
        <br />
        <textarea
          id="message"
          value={message}
          onChange={(event) => setMessage(event.target.value)}
        />

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

## Understanding the Complete Flow

Let's follow the journey of the data.

```text
User Opens /contact
        │
        ▼
React Renders Form
        │
        ▼
User Types "John"
        │
        ▼
onChange Fires
        │
        ▼
setName("John")
        │
        ▼
React State Updates
        │
        ▼
User Clicks Submit
        │
        ▼
onSubmit Fires
        │
        ▼
handleSubmit()
        │
        ▼
event.preventDefault()
        │
        ▼
Read React State
        │
        ▼
Console Output
```

Notice something important:

The submitted values came from **React state**, not directly from the HTML inputs.

This is why we made the inputs **controlled components** in Part 2.

---

## Why Didn't We Read the Values Directly from the Form?

You might wonder:

> "Why don't we just read the values from the `<input>` elements when the user clicks Submit?"

You can do that in plain JavaScript, but in React the recommended pattern is to keep the form values in state.

That gives your component immediate access to the current values for:

* Validation
* Displaying errors
* Sending data to an API
* Resetting the form
* Updating the UI

React state becomes the **single source of truth** for your form.

---

## Common Beginner Mistakes

### 1. Forgetting `onSubmit`

```tsx
<form>
```

If you don't attach `onSubmit`, `handleSubmit()` will never be called.

Always connect them:

```tsx
<form onSubmit={handleSubmit}>
```

#

### 2. Forgetting `event.preventDefault()`

Without it, the browser reloads the page immediately after submission, making it seem like your code didn't work.

#

### 3. Expecting `console.log()` to appear in the terminal

The `console.log()` statements in this component run **in the browser**, so you'll find the output in **Developer Tools → Console**, not in the terminal running `npm run dev`.

---

## Part 3 Summary

Today you learned:

* ✅ How the `onSubmit` event works.
* ✅ How to create a `handleSubmit()` function.
* ✅ What the `event` object is.
* ✅ Why `event.preventDefault()` is necessary.
* ✅ How to access all submitted values from React state.
* ✅ The complete flow from user input to form submission.

At this point, your form can:

* Display fields.
* Store user input in React state.
* Submit without reloading the page.
* Access all entered values.

---

## Next Lab

In **Part 4**, we'll add **client-side validation**:

* Show an error if a required field is empty.
* Validate the email format.
* Display error messages under the correct fields.
* Only allow successful submission when all fields are valid.

This will complete a realistic, production-style contact form before we move on to **Phase 9 — API Routes**.
