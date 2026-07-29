**Phase 2 – React Fundamentals**

# Lesson 7 – Conditional Rendering

So far you've learned:

* ✅ Components
* ✅ JSX
* ✅ Props
* ✅ State
* ✅ Events
* ✅ Rendering Lists

Today we'll learn **Conditional Rendering**.

---

## Goal of This Lesson

By the end of this lesson, you should be able to answer:

* What is conditional rendering?
* Why do we need it?
* How does React decide what to show?
* What is `if` used for?
* What is the ternary operator (`? :`)?
* What is `&&` used for?

That's all.

---

## Before Learning Conditional Rendering...

Imagine you open your banking app.

You are **logged in**.

You see:

```text
Welcome, Baloram

[Account]

[Transfer]

[Logout]
```

Now imagine another person opens the same app.

They are **not logged in**.

They see:

```text
Welcome

[Login]

[Register]
```

Same application.

Different users.

Different screens.

How?

The application checks a **condition**.

---

## What is a Condition?

A condition is simply:

> **A question that can be answered with either "Yes" or "No".**

Examples:

```text
Is the user logged in?

↓

Yes
```

or

```text
Is the user logged in?

↓

No
```

Another example:

```text
Is the shopping cart empty?

↓

Yes
```

or

```text
↓

No
```

React uses these answers to decide what to display.

---

## What is Conditional Rendering?

A simple definition:

> **Conditional Rendering means showing different UI based on a condition.**

Think of it like this:

```text
Condition

↓

React decides

↓

Which UI to display
```

---

## Real-World Analogy

Imagine traffic lights.

If:

```text
Light = Green
```

Cars move.

If:

```text
Light = Red
```

Cars stop.

The condition changes the behavior.

React works the same way.

---

## Another Analogy

Imagine it's raining.

If:

```text
Raining = Yes
```

You take an umbrella.

If:

```text
Raining = No
```

You don't.

The condition decides the action.

React lets a condition decide the UI.

---

## Example 1 — Login Screen

Imagine this variable:

```text
loggedIn = true
```

React shows:

```text
Welcome Back!
```

Now imagine:

```text
loggedIn = false
```

React shows:

```text
Please Login
```

The UI changes because the condition changed.

---

## Example 2 — Shopping Cart

Suppose:

```text
Cart Items = 0
```

React displays:

```text
Your cart is empty.
```

Now the user adds a product.

```text
Cart Items = 1
```

React displays:

```text
Laptop

Checkout
```

Same page.

Different UI.

---

## Example 3 — Loading Data

Imagine a page is downloading information.

Initially:

```text
Loading...
```

When the download finishes:

```text
Products

Product 1

Product 2

Product 3
```

The condition changed.

React displayed different content.

---

## How React Makes Decisions

Think of React like a security guard.

```text
Condition

↓

Can this UI be shown?

↓

Yes

↓

Show it
```

or

```text
Condition

↓

No

↓

Hide it
```

---

## Method 1 – Using `if`

JavaScript already has:

```javascript
if
```

React can use it too.

Imagine:

```text
User is Admin
```

Show:

```text
Admin Panel
```

Otherwise:

Don't show it.

The decision starts with:

```javascript
if (...)
```

You don't need to memorize the syntax today.

Just remember:

`if` helps React choose between different paths.

---

## Method 2 – Ternary Operator (`? :`)

Sometimes the decision is very small.

Instead of writing a full `if`, React often uses a ternary operator.

Think of it like this:

```text
Question ?

↓

Yes

:

No
```

For example:

```text
Is the user logged in?

↓

Yes → Logout

↓

No → Login
```

One question.

Two possible results.

---

## Method 3 – Logical AND (`&&`)

Sometimes you only want to show something **if a condition is true**.

Example:

```text
New Notification
```

If there are notifications:

```text
🔔 5 Notifications
```

If there are none:

Show nothing.

This is where `&&` is useful.

Think of it as:

```text
If True

↓

Show UI

If False

↓

Show Nothing
```

---

## Visual Comparison

### `if`

```text
Condition

↓

Choose Path A

or

Choose Path B
```

#

### Ternary

```text
Question ?

↓

Result A

:

Result B
```

#

### `&&`

```text
Condition

↓

True?

↓

Show UI

↓

False?

↓

Nothing
```

---

## Real Application Example

Imagine an online store.

```text
User visits Product Page
```

React checks:

```text
Is the product in stock?
```

If yes:

```text
[Buy Now]
```

If no:

```text
Out of Stock
```

Another condition:

```text
Is the user logged in?
```

If yes:

```text
Wishlist
```

If no:

```text
Login to Save
```

Multiple conditions can exist on the same page.

---

## How This Fits with State

Remember our previous lesson?

State changes over time.

Now imagine:

```text
loggedIn = false
```

React shows:

```text
Login
```

User logs in.

State changes:

```text
loggedIn = true
```

React re-renders.

Now it shows:

```text
Logout
```

Notice something important.

The **condition didn't change itself**.

The **state changed**.

The condition simply checked the latest state.

---

## Putting It All Together

Let's connect everything you've learned.

```text
Component

↓

Receives Props

↓

Has State

↓

User Triggers Event

↓

State Changes

↓

React Re-renders

↓

Conditions are Checked

↓

Correct UI Appears
```

This is the complete React flow you've been building toward.

---

## Important Rules

### Rule 1

Conditional rendering is simply choosing which UI to display.

#

### Rule 2

Conditions usually come from state or props.

Examples:

* Is the user logged in?
* Is loading complete?
* Is the cart empty?
* Is the user an admin?

#

### Rule 3

React commonly uses:

* `if`
* Ternary (`? :`)
* `&&`

Each has a different purpose.

#

### Rule 4

Changing state can change the result of a condition, which changes what the user sees.

---

## Summary

```text
State or Props

↓

Condition

↓

React Chooses UI

↓

Browser Displays It
```

---

## Mini Quiz

Try answering these without looking back.

### 1.

What is conditional rendering?

#

### 2.

What is a condition?

#

### 3.

What are the three common ways React handles conditional rendering?

#

### 4.

When would you use `&&`?

#

### 5.

What usually causes a condition to change?

#

### 6.

Complete this flow:

```text
State Changes

↓

?

↓

React Chooses UI

↓

Updated Screen
```

---

## What You've Learned So Far

| Step | Concept               | Purpose                                  |
| ---- | --------------------- | ---------------------------------------- |
| 4    | Components            | Build reusable UI                        |
| 5    | JSX                   | Describe UI                              |
| 6    | Props                 | Pass data                                |
| 7    | State                 | Store changing data                      |
| 8    | Events                | Respond to user actions                  |
| 9    | Lists                 | Display repeated data                    |
| 10   | Conditional Rendering | Display different UI based on conditions |

These seven concepts are the **core of React**. Every Next.js application—from a simple blog to a large e-commerce platform—uses them constantly.

---

## Today's Assignment

Be able to explain this flow in your own words:

```text
State or Props

↓

A Condition is Evaluated

↓

React Decides What Should Be Visible

↓

The Browser Shows the Correct UI
```

If you understand that **React doesn't manually show or hide things—you describe the conditions, and React decides what to render**, you've completed today's lesson.

---

## Next Lesson

Before we move into **Phase 3 (App Router)**, I recommend one final React lesson that isn't on the original roadmap:

> **Lesson 8 – The React Rendering Lifecycle**

We'll answer questions like:

* What does "re-render" actually mean?
* Does React reload the whole page?
* When does a component run again?
* What triggers a re-render?
* How does React update only the changed parts of the UI?

Understanding this will make concepts like Server Components, Client Components, and Next.js rendering much easier later. It's a small lesson, but it fills an important gap before we start working with the App Router.
