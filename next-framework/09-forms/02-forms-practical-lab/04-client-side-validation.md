**Phase 8 Practical Lab**

# Part 4 — Client-Side Validation

Current progress:

* ✅ Part 1 — Build the Form UI
* ✅ Part 2 — Controlled Components (`useState`)
* ✅ Part 3 — Handle Form Submission

Now we'll build the final piece before connecting to an API.

---

## Learning Objective

By the end of this lesson, you'll understand:

* How to validate multiple fields
* How to show an error under the correct field
* Why each field should have its own error message
* How to stop form submission when validation fails
* How to allow submission when everything is valid

Today we're going to build a validation flow that behaves like a real application.

---

## Before We Write Code

Suppose the user clicks **Submit** without typing anything.

Current behavior:

```text
Name:
(empty)

Email:
(empty)

Message:
(empty)

↓

Submit

↓

Console Output
```

That's not useful.

Instead, we want:

```text
Name:
(empty)

❌ Name is required.

Email:
(empty)

❌ Email is required.

Message:
(empty)

❌ Message is required.
```

Notice something important.

We don't want **one** error message.

We want **one error for each field**.

---

## Why Not One Error Variable?

Previously we used:

```tsx
const [error, setError] = useState("");
```

Imagine this happens:

```text
Name:
(empty)

Email:
wrong

Message:
(empty)
```

Which error should we show?

```text
Name is required.
```

or

```text
Email is invalid.
```

or

```text
Message is required.
```

One variable can't show three different errors at the same time.

So instead of:

```text
One Error

↓

All Fields
```

we'll use:

```text
Name Error

Email Error

Message Error
```

Each field gets its own validation message.

---

## Step 1 — Create Error State

Under your existing state, add:

```tsx
const [nameError, setNameError] = useState("");
const [emailError, setEmailError] = useState("");
const [messageError, setMessageError] = useState("");
```

Now your component stores:

```text
Name

↓

name

Name Error

↓

nameError

Email

↓

email

Email Error

↓

emailError

Message

↓

message

Message Error

↓

messageError
```

---

## Step 2 — Clear Previous Errors

Every time the user clicks **Submit**, we should start fresh.

At the beginning of `handleSubmit()`:

```tsx
setNameError("");
setEmailError("");
setMessageError("");
```

Why?

Imagine this:

First attempt:

```text
Name:
(empty)
```

Error:

```text
Name is required.
```

User fixes it.

Clicks Submit again.

If we don't clear the previous errors, the old message will still appear.

Always start validation with a clean slate.

---

## Step 3 — Validate the Name

Now add:

```tsx
if (name.trim() === "") {
  setNameError("Name is required.");
}
```

Let's understand it.

`trim()` removes spaces.

Example:

```text
"   John   "
```

becomes

```text
"John"
```

But

```text
"      "
```

becomes

```text
""
```

So someone can't bypass validation by typing only spaces.

---

## Step 4 — Validate the Email

First check if it's empty.

```tsx
if (email.trim() === "") {
  setEmailError("Email is required.");
}
```

Now check the format.

```tsx
else if (!email.includes("@")) {
  setEmailError("Enter a valid email address.");
}
```

For this lesson we're keeping the validation simple.

Later, we'll learn stronger validation patterns.

---

## Step 5 — Validate the Message

Exactly the same idea.

```tsx
if (message.trim() === "") {
  setMessageError("Message is required.");
}
```

---

## Step 6 — Determine Whether the Form Is Valid

Right now we're showing errors.

But we also need to decide:

Should the form continue?

Let's introduce a flag.

```tsx
let isValid = true;
```

Initially we assume:

```text
Everything is valid.
```

Whenever we find a problem:

```tsx
isValid = false;
```

Example:

```tsx
if (name.trim() === "") {
  setNameError("Name is required.");
  isValid = false;
}
```

Do the same for every validation rule.

---

## Step 7 — Stop Invalid Submissions

At the end of validation:

```tsx
if (!isValid) {
  return;
}
```

Meaning:

```text
Validation Failed

↓

Stop Here

↓

Do NOT Continue
```

Only when every check passes do we continue.

---

## Step 8 — Successful Submission

Now we can safely write:

```tsx
console.log("Form submitted successfully");

console.log(name);
console.log(email);
console.log(message);
```

Notice the difference.

Before:

```text
Every click

↓

Console
```

Now:

```text
Invalid Form

↓

Show Errors

↓

STOP
```

Only

```text
Valid Form

↓

Console
```

---

## Step 9 — Display Errors

Under the Name input:

```tsx
{nameError && (
  <p>{nameError}</p>
)}
```

Remember this from Phase 2.

If:

```text
nameError = ""
```

Nothing appears.

If:

```text
nameError = "Name is required."
```

React renders:

```text
Name is required.
```

Do the same for Email.

```tsx
{emailError && (
  <p>{emailError}</p>
)}
```

And Message.

```tsx
{messageError && (
  <p>{messageError}</p>
)}
```

Now every field displays its own message.

---

## Validation Flow

```text
User Clicks Submit
          │
          ▼
Clear Old Errors
          │
          ▼
Check Name
          │
          ▼
Check Email
          │
          ▼
Check Message
          │
          ▼
Any Errors?
     │
 ┌───┴────┐
 │        │
Yes       No
 │        │
 ▼        ▼
Show      Continue
Errors    Submission
```

---

## Example 1

User enters:

```text
Name:

Email:

Message:
```

Result:

```text
❌ Name is required.

❌ Email is required.

❌ Message is required.
```

---

## Example 2

User enters:

```text
Name: John

Email: johngmail.com

Message: Hello
```

Result:

```text
❌ Enter a valid email address.
```

---

## Example 3

User enters:

```text
Name: John

Email: john@gmail.com

Message: Hello
```

Result:

```text
Form submitted successfully

John

john@gmail.com

Hello
```

---

## Why This Approach?

Notice we separated responsibilities.

```text
State

↓

Stores Values
```

```text
Validation

↓

Checks Values
```

```text
Errors

↓

Displays Problems
```

Each part has one job.

This makes the code easier to understand and maintain.

---

## Common Beginner Mistakes

### 1. Using one error variable

```tsx
const [error, setError] = useState("");
```

This works for very small examples but doesn't scale when you have multiple fields.

#

### 2. Returning too early

Some beginners write:

```tsx
if (name.trim() === "") {
  return;
}
```

The rest of the fields are never checked.

It's better to validate **all fields** and show all relevant errors at once.

#

### 3. Forgetting to reset previous errors

Always clear existing error messages before running validation again.

---

## Part 4 Summary

Today you learned:

* ✅ How to validate multiple fields.
* ✅ Why each field should have its own error state.
* ✅ How to use an `isValid` flag to control submission.
* ✅ How to display field-specific error messages.
* ✅ How to prevent invalid form submissions.
* ✅ How to continue only when every validation rule passes.

---

## Phase 8 Practical Lab Status

* ✅ Part 1 — Build the UI
* ✅ Part 2 — Controlled Components
* ✅ Part 3 — Handle Submission
* ✅ Part 4 — Client-Side Validation

At this point, you have a realistic contact form that:

* Displays correctly.
* Stores user input in React state.
* Handles form submission without reloading the page.
* Validates all fields.
* Shows errors under the correct inputs.
* Only proceeds when the form is valid.

This will give you a polished, production-style contact form while still staying entirely within **Phase 8**. After that, we'll naturally connect it to a real API in Phase 9.
