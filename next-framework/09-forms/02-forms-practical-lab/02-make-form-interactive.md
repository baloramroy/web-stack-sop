**Phase 8 Practical Lab**

# Part 2 — Make the Form Interactive with React State

## Learning Objective

By the end of this lesson, you'll understand:

* Why we need `"use client"`
* What controlled components are
* How `useState` stores form data
* How `value` and `onChange` work together
* How React updates the UI as the user types

**Today we are NOT submitting the form yet.**

Our only goal is:

```text
User Types

↓

React Stores Every Character
```

---

## Before Writing Code

Let's think about what happens today.

Suppose the user types:

```text
John
```

into this input:

```tsx
<input type="text" />
```

Who knows that the value is "John"?

The answer is:

```text
The Browser
```

React doesn't automatically know.

The browser stores it internally.

```
Browser

↓

Input

↓

John
```

If we want to use that value later (for validation or submission), **React needs to know it too**.

---

## The Solution

React stores data in something called **State**.

Think of State as the component's memory.

```
User Types

↓

React State

↓

Component Knows the Value
```

---

## Why Do We Need `"use client"`?

Open your page.

Currently it looks like:

```tsx
export default function ContactPage() {
```

We're about to use:

* `useState`
* `onChange`
* User events

These only work in a **Client Component**.

So the first line becomes:

```tsx
"use client";
```

Your file now starts with:

```tsx
"use client";

export default function ContactPage() {
```

---

## Why?

Remember Phase 6?

You learned there are two types of components.

```
Server Component

Client Component
```

Server Components cannot:

* useState
* onClick
* onChange
* onSubmit

Client Components can.

That's why we add:

```tsx
"use client";
```

---

## Step 1 — Import `useState`

Under `"use client"`:

```tsx
import { useState } from "react";
```

Now React gives us access to State.

---

## Step 2 — Create State

Let's start with the Name field.

```tsx
const [name, setName] = useState("");
```

This line is very important.

Let's break it apart.

#

### What is `useState("")`?

The empty string:

```tsx
""
```

means:

> "Initially, the Name field is empty."

So before the user types anything:

```
name

↓

""
```

#

### Why Two Variables?

This often confuses beginners.

```tsx
const [name, setName] = useState("");
```

Think of it like this:

```
name

↓

Current Value
```

and

```
setName()

↓

Update the Value
```

For example:

Initially:

```
name

↓

""
```

Then:

```tsx
setName("John");
```

Now:

```
name

↓

"John"
```

React automatically remembers the new value.

---

## Step 3 — Connect the Input

Currently your input looks like:

```tsx
<input
  id="name"
  type="text"
/>
```

Let's connect it to React.

```tsx
<input
  id="name"
  type="text"
  value={name}
  onChange={(event) => setName(event.target.value)}
/>
```

This introduces two new props.

---

## What Does `value={name}` Mean?

This tells React:

> "Display whatever is stored in `name`."

Initially:

```
name

↓

""
```

The input is empty.

If later:

```
name

↓

"John"
```

the input automatically shows:

```
John
```

---

## What Does `onChange` Do?

Every time the user types a character:

```
J

↓

Jo

↓

Joh

↓

John
```

React runs:

```tsx
onChange={(event) => setName(event.target.value)}
```

Let's see it step by step.

---

## User Types

User presses:

```
J
```

The browser now contains:

```
J
```

React receives an event.

Inside that event:

```tsx
event.target.value
```

contains:

```
"J"
```

Then:

```tsx
setName("J")
```

updates the state.

Now:

```
name

↓

"J"
```

#

User types another letter.

```
Jo
```

React receives:

```tsx
event.target.value
```

which is:

```
"Jo"
```

Then:

```tsx
setName("Jo")
```

updates the state again.

This happens for **every keystroke**.

---

## The Complete Flow

```
User presses key
        │
        ▼
Browser updates input
        │
        ▼
onChange fires
        │
        ▼
event.target.value
        │
        ▼
setName(...)
        │
        ▼
React State updates
        │
        ▼
Input displays latest value
```

This happens so quickly that it feels instantaneous.

---

## Step 4 — Add State for Email

Create another state variable.

```tsx
const [email, setEmail] = useState("");
```

Connect the input.

```tsx
<input
  id="email"
  type="email"
  value={email}
  onChange={(event) => setEmail(event.target.value)}
/>
```

Exactly the same pattern.

---

## Step 5 — Add State for Message

Create:

```tsx
const [message, setMessage] = useState("");
```

Then connect the textarea.

```tsx
<textarea
  id="message"
  value={message}
  onChange={(event) => setMessage(event.target.value)}
></textarea>
```

Now all three fields are controlled by React.

---

## Complete Code

```tsx
"use client";

import { useState } from "react";

export default function ContactPage() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [message, setMessage] = useState("");

  return (
    <main>
      <h1>Contact Us</h1>

      <form>
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

        <button type="submit">Submit</button>
      </form>
    </main>
  );
}
```

---

## What Have We Achieved?

Before today:

```
User Types

↓

Browser Knows
```

React had no access to the values.

After today's lesson:

```
User Types

↓

Browser

↓

onChange

↓

React State

↓

Component Knows Everything
```

Now your component always knows:

* The current name
* The current email
* The current message

This is the foundation for everything that comes next.

---

## Common Beginner Mistakes

### 1. Forgetting `"use client"`

If you remove it, Next.js will report an error because `useState` and event handlers require a Client Component.

#

### 2. Providing `value` without `onChange`

```tsx
<input value={name} />
```

The input becomes read-only because React controls its value but never updates it.

#

### 3. Updating State Directly

❌ Incorrect:

```tsx
name = "John";
```

React won't know it needs to re-render.

✔ Correct:

```tsx
setName("John");
```

Always use the setter function returned by `useState`.

---

## Part 2 Summary

Today you learned:

* ✅ Why `"use client"` is required.
* ✅ How `useState` stores form data.
* ✅ The difference between a state value (`name`) and its setter (`setName`).
* ✅ How `value` connects the input to React state.
* ✅ How `onChange` updates the state with every keystroke.
* ✅ What a **controlled component** is.

Your form is now **interactive**. Every character the user types is stored in React state.

---

## Next Lab

In **Part 3**, we'll make the form actually **submit**:

* Add `onSubmit` to the form.
* Create a `handleSubmit()` function.
* Learn the `event` object.
* Use `event.preventDefault()`.
* Display all submitted values in the browser console.

By the end of Part 3, you'll understand the complete submission flow before we add validation and connect the form to an API.
