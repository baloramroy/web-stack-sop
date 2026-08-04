**Phase 8 Practical Lab**

# Part 5 — Build a Production-Style Contact Form

After today, your contact form will behave much more like a real application.

Current progress:

* ✅ Part 1 – Build the UI
* ✅ Part 2 – React State
* ✅ Part 3 – Handle Form Submission
* ✅ Part 4 – Client-side Validation

Today we'll add the final polish.

---


## Learning Objectives

By the end of this lesson, you'll understand:

* How to display a success message
* How to clear the form after a successful submission
* How to simulate a request with a loading state
* Why we disable the submit button
* Why components should be separated into reusable files

> **We are still NOT calling an API.**
>
> We'll simulate a request so that Phase 9 focuses only on API Routes.

---

## Before We Write Code

Think about a real website.

You fill out a contact form.

```
Name: John

Email: john@gmail.com

Message: Hello
```

You click:

```
Submit
```

Does the website instantly respond?

Usually not.

Instead, you see something like:

```
Submitting...
```

A second later:

```
✅ Message sent successfully!
```

Your form becomes empty again.

That is exactly what we'll build today.

---

## Step 1 — Add New State

Currently we have:

```tsx
const [name, setName] = useState("");
const [email, setEmail] = useState("");
const [message, setMessage] = useState("");

const [nameError, setNameError] = useState("");
const [emailError, setEmailError] = useState("");
const [messageError, setMessageError] = useState("");
```

Now let's add two more.

```tsx
const [isSubmitting, setIsSubmitting] = useState(false);

const [successMessage, setSuccessMessage] = useState("");
```

#

### What is `isSubmitting`?

Initially:

```
false
```

Meaning:

```
The form is idle.
```

Later:

```
true
```

Means:

```
The form is currently submitting.
```

Think of it as a light switch.

```
false

↓

Idle
```

```
true

↓

Working...
```

#

### What is `successMessage`?

Initially:

```text
""
```

Nothing is displayed.

Later:

```text
"Your message has been sent successfully!"
```

React automatically displays it.

---

## Step 2 — Simulate an API Request

Since we don't know APIs yet,

we'll pretend an API takes **2 seconds**.

Inside `handleSubmit()` after validation succeeds:

```tsx
setIsSubmitting(true);
```

Meaning:

```
User Clicks Submit

↓

Loading Starts
```

Now add:

```tsx
await new Promise((resolve) =>
  setTimeout(resolve, 2000)
);
```

Let's understand this.

#

### What does `setTimeout()` do?

It waits.

```text
Start

↓

Wait 2 Seconds

↓

Continue
```

We're pretending the server is processing our request.

Later,

instead of this fake delay,

we'll replace it with:

```tsx
await fetch(...)
```

during Phase 9.

---

## Step 3 — Why Do We Need `async`?

Because we're using:

```tsx
await
```

our function must become:

```tsx
async function handleSubmit(
  event: React.FormEvent<HTMLFormElement>
) {
```

Without `async`, JavaScript doesn't allow `await`.

---

## Step 4 — Show Success

After the fake delay:

```tsx
setSuccessMessage(
  "Your message has been sent successfully!"
);
```

Now React knows:

```
Show

↓

Success Message
```

---

## Step 5 — Clear the Form

Right after success:

```tsx
setName("");
setEmail("");
setMessage("");
```

Think about what happens.

Before:

```
Name

↓

John
```

After:

```
Name

↓

""
```

React automatically clears the input because the input is controlled by state.

Remember Part 2?

```
Input

↓

State

↓

Input
```

When the state changes,

the UI changes.

---

## Step 6 — Stop Loading

Finally:

```tsx
setIsSubmitting(false);
```

Flow:

```
Submit

↓

Loading

↓

Finished

↓

Normal Again
```

---

## Step 7 — Disable the Button

Currently:

```tsx
<button type="submit">
    Submit
</button>
```

Let's improve it.

```tsx
<button
  type="submit"
  disabled={isSubmitting}
>
  {isSubmitting
    ? "Submitting..."
    : "Submit"}
</button>
```

This introduces two new ideas.

#

### The `disabled` Property

When

```text
isSubmitting = true
```

the browser automatically prevents clicking.

```
[Submitting...]

(Cannot Click)
```

When

```text
false
```

```
[Submit]
```

works normally.

#

### Conditional Text

Instead of always showing:

```
Submit
```

we ask React:

```tsx
isSubmitting
  ? "Submitting..."
  : "Submit"
```

Meaning:

```
Is Loading?

↓

Yes

↓

Submitting...
```

Otherwise:

```
Submit
```

---

## Step 8 — Display the Success Message

Above the form:

```tsx
{successMessage && (
  <p>{successMessage}</p>
)}
```

Exactly the same idea as validation.

Initially:

```
successMessage

↓

""
```

Nothing appears.

After submission:

```
successMessage

↓

Your message has been sent successfully!
```

React renders:

```
✅ Your message has been sent successfully!
```

---

## Complete Submission Flow

```
User
 │
 ▼
Fill Form
 │
 ▼
Submit
 │
 ▼
Validation
 │
 ▼
No Errors
 │
 ▼
Loading Starts
 │
 ▼
Button Disabled
 │
 ▼
Wait 2 Seconds
 │
 ▼
Success Message
 │
 ▼
Clear Form
 │
 ▼
Loading Ends
```

This is almost identical to what a real application does.

The only missing piece is the actual API request.

---

## Step 9 — Organize the Code

Right now everything lives in:

```
src/app/contact/page.tsx
```

It works,

but imagine your form grows to 300 lines.

Your page becomes difficult to read.

Instead we'll organize it like this:

```
src/
│
├── app/
│   └── contact/
│       └── page.tsx
│
└── components/
    └── ContactForm.tsx
```

---

### What Goes in `page.tsx`?

Its job is simply to render the page.

```tsx
import ContactForm from "@/components/ContactForm";

export default function ContactPage() {
  return (
    <main>
      <h1>Contact Us</h1>
      <ContactForm />
    </main>
  );
}
```

Notice how clean it becomes.

---

### What Goes in `ContactForm.tsx`?

Everything related to the form:

* State
* Inputs
* Validation
* Submission
* Success message
* Loading state

This component now has **one responsibility**: managing the contact form.

---

## Why Split Components?

Imagine a page with:

* Contact Form
* Google Map
* FAQ
* Company Information
* Footer

Putting all of that into one file quickly becomes hard to manage.

Instead:

```
Contact Page
│
├── ContactForm
├── GoogleMap
├── FAQ
└── Footer
```

Each component is responsible for one part of the page.

This makes the code:

* Easier to read
* Easier to test
* Easier to reuse
* Easier to maintain

---

## What We Built

Your contact form now has many features found in production applications:

* ✅ Controlled inputs using React state.
* ✅ Form submission handled with `onSubmit`.
* ✅ Client-side validation.
* ✅ Field-specific error messages.
* ✅ Loading state while processing.
* ✅ Disabled submit button during submission.
* ✅ Success message after completion.
* ✅ Automatic form reset.
* ✅ A clean component structure.

---

## What We Are Simulating

Today:

```
Submit

↓

Wait 2 Seconds

↓

Success
```

Next Phase:

```
Submit

↓

POST /api/contact

↓

Next.js API Route

↓

Response

↓

Success
```

The user experience will feel almost identical. The difference is that, in **Phase 9**, the 2-second delay will be replaced with a real HTTP request handled by your own Next.js backend.

---

## 🎉 Phase 8 Practical Lab Completed

Congratulations! You now understand the complete lifecycle of a modern React form:

1. Build the UI.
2. Store user input in state.
3. Handle submission.
4. Validate the data.
5. Provide user feedback.
6. Reset the form.
7. Organize the code into reusable components.

Because you already understand this workflow, **Phase 9 – API Routes** will feel much more natural. Instead of introducing both forms and networking at the same time, you'll only have one new concept to learn: how the submitted data travels from your React form to a Next.js API Route and back.
