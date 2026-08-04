**Phase 8 — Forms**

# Step 3 — Validation

Completed:

* ✅ Step 29 — Create Forms
* ✅ Step 30 — Handle Form Submission

Now we begin the final lesson of this phase.

---

## Learning Objective

By the end of this lesson, you'll understand:

* What validation is
* Why validation is important
* How to validate user input in React/Next.js
* How to show validation errors
* When to allow form submission

> **Today we are only validating the form on the client side.**
>
> We are **not** sending data to an API yet. That will happen in **Phase 9 — API Routes**. 

---

## What Is Validation?

Validation means checking whether the user's input is acceptable **before** processing it.

Suppose a contact form asks for:

* Name
* Email

A user enters:

```text
Name: John
Email: john@example.com
```

Everything looks good.

Now another user enters:

```text
Name:
Email: abc
```

Problems:

* Name is empty.
* Email is not a valid email address.

Validation catches these problems before moving on.

---

## Real-Life Example

Imagine you're registering for a new account.

The website asks for:

```text
Name

Email

Password
```

If you leave everything blank and click **Register**, the website doesn't create your account.

Instead, it says things like:

```text
Name is required.

Email is required.

Password must be at least 8 characters.
```

That's validation.

---

## Where Does Validation Fit?

Let's review the form flow.

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
Validation
 │
 ├──────────────┐
 │              │
Valid       Invalid
 │              │
 ▼              ▼
Next Step   Show Errors
```

Notice something important.

Validation happens **before** the form moves to the next step.

---

## Our Contact Form

Let's extend our previous example.

We'll collect:

* Name
* Email

```tsx
"use client";

import { useState } from "react";

export default function ContactPage() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");

  return (
    <form>
      ...
    </form>
  );
}
```

---

## What Should We Validate?

For this lesson, we'll use two simple rules.

### Name

Must not be empty.

✔ Valid

```text
John
```

❌ Invalid

```text
```

#

### Email

Must:

* Not be empty.
* Contain the `@` symbol.

✔ Valid

```text
john@gmail.com
```

❌ Invalid

```text
johngmail.com
```

Later in your journey, you'll learn stronger validation techniques, but these rules are enough to understand the concept.

---

## Creating an Error State

Besides storing the input values, we also need somewhere to store error messages.

```tsx
const [error, setError] = useState("");
```

Now our component has three pieces of state:

```text
Name

↓

name

Email

↓

email

Validation Message

↓

error
```

---

## Validating on Submit

Update the submit function.

```tsx
function handleSubmit(event) {
  event.preventDefault();

  if (name.trim() === "") {
    setError("Name is required.");
    return;
  }

  if (email.trim() === "") {
    setError("Email is required.");
    return;
  }

  if (!email.includes("@")) {
    setError("Enter a valid email address.");
    return;
  }

  setError("");

  console.log("Form is valid");
}
```

Let's understand this step by step.

---

## First Check

```tsx
if (name.trim() === "") {
```

`trim()` removes spaces from the beginning and end.

Example:

```text
"   John   "
```

becomes:

```text
"John"
```

If the user only types spaces:

```text
"      "
```

`trim()` produces:

```text
""
```

which counts as empty.

---

## Second Check

```tsx
if (email.trim() === "") {
```

The email field cannot be empty.

---

## Third Check

```tsx
if (!email.includes("@")) {
```

We're checking whether the email contains:

```text
@
```

Example:

✔

```text
john@gmail.com
```

❌

```text
johngmail.com
```

Remember, this is just a simple learning example.

---

## Showing the Error

Right now, we're storing the error message.

Let's display it.

```tsx
{
  error && <p>{error}</p>
}
```

What does this mean?

```tsx
error && <p>{error}</p>
```

is called **conditional rendering**.

You learned this earlier in the roadmap.

If:

```text
error = ""
```

nothing appears.

If:

```text
error = "Name is required."
```

the browser shows:

```text
Name is required.
```

---

## Complete Example

```tsx
"use client";

import { useState } from "react";

export default function ContactPage() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [error, setError] = useState("");

  function handleSubmit(event) {
    event.preventDefault();

    if (name.trim() === "") {
      setError("Name is required.");
      return;
    }

    if (email.trim() === "") {
      setError("Email is required.");
      return;
    }

    if (!email.includes("@")) {
      setError("Enter a valid email address.");
      return;
    }

    setError("");

    console.log("Form is valid");
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

        <label>Email</label>
        <br />
        <input
          type="email"
          value={email}
          onChange={(event) => setEmail(event.target.value)}
        />

        <br />
        <br />

        {error && <p>{error}</p>}

        <button type="submit">
          Submit
        </button>
      </form>
    </main>
  );
}
```

---

## What Happens Now?

Suppose the user submits:

```text
Name:

Email:
```

The flow is:

```text
Click Submit
      │
      ▼
handleSubmit()
      │
      ▼
Name empty?
      │
      ▼
Yes
      │
      ▼
Show

"Name is required."
```

Another example:

```text
Name: John

Email: abc
```

Flow:

```text
Submit
   │
   ▼
Email contains @ ?
   │
   ▼
No
   │
   ▼
Show

"Enter a valid email address."
```

Valid input:

```text
Name: John

Email: john@gmail.com
```

Flow:

```text
Submit
   │
   ▼
All checks pass
   │
   ▼
Console

"Form is valid"
```

---

## Why Validate on the Client?

Client-side validation improves the user experience.

Instead of submitting incorrect data and waiting for a response, users get immediate feedback.

However, it's important to understand:

> **Client-side validation is not enough for security.**

When we reach **Phase 9 — API Routes**, you'll learn that the server should also validate incoming data before using or storing it.

---

## Common Beginner Mistakes

### 1. Forgetting `event.preventDefault()`

The page reloads before your validation runs.

#

### 2. Forgetting to clear old errors

If validation succeeds, remember to remove the previous message.

```tsx
setError("");
```

#

### 3. Trusting only the browser

Even though you're validating in the browser, the server must validate the data again. We'll cover that when we build API Routes.

---

## Step 3 Summary

Today you learned:

* ✅ What validation is.
* ✅ Why validation is important.
* ✅ How to validate form input in a Next.js application.
* ✅ How to store validation messages in React state.
* ✅ How to display errors using conditional rendering.
* ✅ Why client-side validation improves user experience but does not replace server-side validation.

---

# 🎉 Phase 8 Completed

Congratulations! You have completed the entire **Forms** phase of your Next.js roadmap. 

You can now:

* Create forms.
* Handle form submissions.
* Read user input with React state.
* Prevent the browser's default form behavior.
* Perform basic client-side validation.
* Display validation errors to users.

## Next Phase

We'll move to **Phase 9 — API Routes**, where you'll learn how a Next.js application creates its own backend endpoints (`GET`, `POST`, `PUT`, and `DELETE`) so your forms can communicate with a server, exactly as outlined in your roadmap. 
