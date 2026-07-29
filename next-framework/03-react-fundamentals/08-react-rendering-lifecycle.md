**Phase 2 – React Fundamentals**

# Lesson 8 – The React Rendering Lifecycle

Many beginners hear the words:

> "React re-renders the component."

...without ever learning what that actually means.

Once you understand this lesson, many things in Next.js will start making sense.

---

## Goal of This Lesson

By the end of this lesson, you should be able to answer:

* What does "render" mean?
* What does "re-render" mean?
* Does React reload the page?
* When does a component run again?
* What triggers a re-render?
* How does React update only what changed?

That's all.

We won't discuss performance optimization or hooks like `useEffect` today.

---

## Before Learning Re-rendering...

Imagine you have this simple page:

```text
------------------------

Count: 0

[ Increment ]

------------------------
```

You click the button.

Now it shows:

```text
------------------------

Count: 1

[ Increment ]

------------------------
```

A question:

> **Did React rebuild the entire webpage?**

Or...

> **Did React update only the number?**

The answer is very important.

---

## What Does "Render" Mean?

A simple definition:

> **Render means creating the UI that should appear on the screen.**

Imagine a painter.

Someone asks:

> "Paint a house."

The painter creates the picture.

That is the first render.

---

## First Render

When your application starts:

```text
Browser Opens

↓

React Starts

↓

Component Runs

↓

UI is Created

↓

Browser Displays It
```

This is called the **Initial Render**.

---

## What is a Re-render?

Now imagine something changes.

For example:

```text
Count

0

↓

1
```

React needs to update the UI.

It runs the component again.

This is called a **Re-render**.

Simple definition:

> **A re-render means React runs the component again to calculate what the UI should look like now.**

Notice the wording:

React **runs the component again**.

It doesn't necessarily redraw the whole page.

---

## Important Idea

Many beginners think:

```text
State Changed

↓

Entire Website Reloads
```

❌ Wrong.

What actually happens is:

```text
State Changed

↓

Component Runs Again

↓

React Compares

↓

Updates Only What's Different
```

---

## Real-World Analogy

Imagine a newspaper editor.

The newspaper has 100 pages.

Someone finds one spelling mistake on page 42.

Does the editor rewrite all 100 pages?

Of course not.

The editor changes only page 42.

React works the same way.

---

## Another Analogy

Imagine Microsoft Word.

You change one word.

```text
Hello

↓

Hi
```

Word doesn't recreate the entire document.

It updates only the changed part.

React follows a similar idea.

---

## Let's Follow a Complete Flow

Imagine this state:

```text
Count = 0
```

The page displays:

```text
Count: 0
```

The user clicks:

```text
Increment
```

Flow:

```text
User Click

↓

Event Handler Runs

↓

State Changes

↓

Component Runs Again

↓

React Compares Old UI

↓

React Finds Difference

↓

Browser Updates

↓

Count: 1
```

Notice:

The browser didn't reload.

Only the changed part was updated.

---

## What Triggers a Re-render?

React doesn't randomly re-render.

Something must trigger it.

The most common triggers are:

### 1. State Changes

Example:

```text
Count

0

↓

1
```

React re-renders.

This is the most common trigger.

#

### 2. Props Change

Imagine:

Parent Component

sends

```text
Name = Alice
```

Later it sends:

```text
Name = Bob
```

The child component receives new props.

React re-renders that child.

#

### 3. Parent Re-renders

Imagine:

```text
Parent

↓

Child
```

If the parent re-renders, React may also run the child again.

We'll learn later that React has ways to optimize this, but for now just remember the basic idea.

---

## What Does NOT Trigger a Re-render?

Suppose you have a normal JavaScript variable.

```javascript
let count = 0;
```

Later:

```javascript
count = 1;
```

React doesn't know anything changed.

No re-render happens.

That's why we learned **state** in the previous lesson.

React watches state, not ordinary variables.

---

## Visual Comparison

### Normal Variable

```text
Variable Changes

↓

React Doesn't Know

↓

No UI Update
```

#

### State

```text
State Changes

↓

React Knows

↓

Component Runs Again

↓

UI Updates
```

---

## Does React Reload the Entire Page?

This is one of the biggest misconceptions.

Imagine you're on an online shopping site.

You click:

```text
Add to Cart
```

The cart changes from:

```text
Cart: 0
```

to

```text
Cart: 1
```

Did the logo disappear?

No.

Did the navigation reload?

No.

Did the footer reload?

No.

Only the cart number changed.

---

## React's Job

Think of React as a smart editor.

```text
Old UI

↓

New UI

↓

Compare

↓

Update Only Differences
```

This is one of the reasons React applications feel fast.

---

## A Bigger Example

Imagine this page.

```text
--------------------------------

Logo

Navigation

Search

Products

Footer

--------------------------------
```

The user clicks:

```text
Like Product
```

Only this changes:

```text
❤️

↓

❤️❤️
```

React doesn't rebuild:

* Logo
* Navigation
* Footer

It updates only what changed.

---

## How Does React Know What Changed?

Today, you only need the basic idea.

React compares:

```text
Previous UI

↓

Current UI
```

It asks:

> "What's different?"

Then it updates only those parts.

Later, when you're more advanced, you'll learn about the **Virtual DOM**, which helps React do this efficiently.

For now, it's enough to know that React compares the old and new UI before updating the browser.

---

## Putting Everything Together

Let's connect every lesson you've learned.

```text
Component

↓

Receives Props

↓

Contains State

↓

User Performs Action

↓

Event Handler Runs

↓

State Changes

↓

Component Re-renders

↓

React Compares UI

↓

Browser Updates Only the Changed Parts
```

This is the complete React lifecycle you've been building toward.

---

## Mental Model

Think of a restaurant kitchen.

A customer changes one item in an order.

Original:

```text
Burger

Fries

Cola
```

New order:

```text
Burger

Salad

Cola
```

The kitchen doesn't remake everything.

It only replaces the fries with the salad.

React behaves the same way.

---

## Important Rules

### Rule 1

The first time a component appears, React **renders** it.

#

### Rule 2

When state or props change, React **re-renders** it.

#

### Rule 3

A re-render means the component function runs again.

#

### Rule 4

A re-render does **not** mean the whole page reloads.

#

### Rule 5

React updates only the parts of the UI that changed.

---

## Summary

```text
Application Starts

↓

Initial Render

↓

User Interaction

↓

State or Props Change

↓

Re-render

↓

React Compares Old UI

↓

Browser Updates Only Differences
```

---

## Mini Quiz

Try answering these without looking back.

### 1.

What is a render?

#

### 2.

What is a re-render?

#

### 3.

Does React reload the whole page after a state change?

#

### 4.

Name two things that commonly trigger a re-render.

#

### 5.

Do normal JavaScript variables trigger a re-render?

#

### 6.

Complete this flow:

```text
User Click

↓

Event Handler

↓

?

↓

Component Runs Again

↓

React Compares UI

↓

Browser Updates
```

---

## What You've Learned in Phase 2

Congratulations! You've completed the **React Fundamentals** phase.

| Step | Concept               | Why It Matters                               |
| ---- | --------------------- | -------------------------------------------- |
| 4    | Components            | Build reusable UI blocks                     |
| 5    | JSX                   | Describe UI with HTML-like syntax            |
| 6    | Props                 | Pass data between components                 |
| 7    | State                 | Store changing data                          |
| 8    | Events                | Respond to user actions                      |
| 9    | Rendering Lists       | Display collections of data                  |
| 10   | Conditional Rendering | Show different UI based on conditions        |
| 11   | Rendering Lifecycle   | Understand how and when React updates the UI |

These concepts are the foundation of every React and Next.js application.

---

## Before We Move to Phase 3

I'd like to point out something important.

When we started, you were learning **React concepts**, not **Next.js features**.

Now that you understand these concepts, you already know enough React to understand why a Next.js page behaves the way it does.

That means we can finally start learning **Next.js itself**.

---

## Next Phase

### Phase 3 – Understanding the Next.js App Router

Our first lesson will be:

### Step 1 – Your First Next.js Page

We'll answer:

* What is the App Router?
* Why is the `app` folder special?
* What is `page.tsx`?
* Why does creating a folder create a URL?
* How does Next.js turn folders into routes?

This is where you'll start connecting everything you've learned about React to how Next.js builds real applications. We'll continue at the same slow, step-by-step pace.
