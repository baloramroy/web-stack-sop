**Phase 2 – React Fundamentals**

# Step 7 – Understanding State (`useState`)

## Goal of This Lesson

By the end of this lesson, you should be able to answer:

* What is state?
* Why do we need state?
* What's the difference between props and state?
* Why does changing state update the UI automatically?
* What is `useState`?

That's all.

We won't write complex code or discuss `useEffect` yet.

---

## Before Learning State...

Imagine you're building a counter application.

- When the page first loads, it shows:

  ```text
  Count: 0
  ```

You click a button.

- Now it should show:

  ```text
  Count: 1
  ```

  Click again:

  ```text
  Count: 2
  ```

  Click again:

  ```text
  Count: 3
  ```

- The UI changes while the application is running.
- Where does React remember the current value?
- That's exactly what **state** is for.

---

## What is State?

A simple definition:

> **State is data that belongs to a component and can change over time.**

Let's break that down.

* It belongs to the component.
* It can change.
* When it changes, the UI updates.

---

## Real-World Analogy: A Whiteboard

Imagine a classroom.

- There is a whiteboard.

- Initially it says:

  ```text
  Students Present: 25
  ```

- Later another student arrives.

- Now the whiteboard becomes:

  ```text
  Students Present: 26
  ```

- The whiteboard keeps changing.
- Think of the whiteboard as **state**.
- It stores the **current value**.

---

## Another Analogy: A Scoreboard

Imagine a football match.

- At the beginning:

  ```text
  Home 0 - 0 Away
  ```

- Then a goal is scored.

  ```text
  Home 1 - 0 Away
  ```

- Another goal.

  ```text
  Home 1 - 1 Away
  ```

- The scoreboard always shows the **latest score**.
- That latest score is like state.

---

## Why Not Use a Normal Variable?

Suppose you write:

```javascript
let count = 0;
```

Then later:

```javascript
count = count + 1;
```

- Now `count` is `1`.
- **JavaScript** knows the **value changed**.
- But React doesn't automatically know, it should update what's on the screen or not.
- React needs a special way to **track values** that affect the UI.

That's why **state** exists.

---

## React's Solution

React says:

> "If a value can change and should update the value on the screen, store it in **state**."

---

## What is `useState`?

- `useState` is a React Hook.
- Don't worry about the word **Hook** yet.
- For today, think of it like this:
  > **`useState` lets a component remember values between each renders.**
- That's all you need to remember for now.

---

## Your First State Example

```jsx
const [count, setCount] = useState(0);
```

- This line might look strange.
- Don't panic.
- We'll read it piece by piece.

#

### Part 1

```jsx
useState(0)
```

- This tells React:

  > "Create a piece of state."

- The initial value is:

  ```text
  0
  ```

#

### Part 2

```jsx
count
```

This is the current value.

- Initially:

  ```text
  0
  ```

- Later it might become:

  ```text
  1
  ```

- Then:

  ```text
  2
  ```

#

### Part 3

```jsx
setCount
```

- This is a function.
- Its job is to change the state.
- Think of it as:

  ```text
  setCount()

  ↓

  Update count

  ↓

  Update UI
  ```

---

## Visual Flow

- When the page loads:

  ```text
  count

  ↓

  0

  ↓

  UI

  ↓

  Count: 0
  ```

- User clicks a button.

  ```text
  setCount(1)

  ↓

  count becomes 1

  ↓

  React re-renders

  ↓

  Count: 1
  ```

---

# Why Does the UI Update Automatically?

- This is React's biggest advantage.
- Imagine this flow:

  ```text
  State Changes

  ↓

  React Notices

  ↓

  React Re-renders Component

  ↓

  Browser Updates
  ```

- You don't manually change the HTML.
- React does it for you.

---

## Props vs State

This is a very important comparison.

| Props                          | State                                 |
| ------------------------------ | ------------------------------------- |
| Passed from a parent component | Belongs to the current component      |
| Read-only                      | Can change                            |
| Parent controls the value      | Component controls the value          |
| Used to pass information       | Used to remember changing information |

Think of it this way:

### Props

- Someone gives you a book.
- You can read it.
- You shouldn't rewrite it.

#

### State

- You own a notebook.
- You can write.
- Erase.
- Update.
- Add new notes.
- The notebook belongs to you.
- That's state.

---

## Another Example

### Imagine a login form.

Initially:

```text
Username:

Password:
```

As the user types:

```text
Username: Baloram
```

Every key press changes the value.

Where is that value stored?

In **state**.

#

### Or imagine a shopping cart.

Initially:

```text
Items: 0
```

Add one product.

```text
Items: 1
```

Add another.

```text
Items: 2
```

The changing number is state.

---

## Mental Model

```text
User Action

↓

State Changes

↓

React Detects Change

↓

Component Re-renders

↓

Screen Updates
```

This is one of the core ideas of React.

---

## Important Rules

### Rule 1

Use state for data that changes.

Examples:

* Counter
* Shopping cart total
* Form input
* Current theme
* Logged-in user (in some cases)

#

### Rule 2

- Don't change state directly.
- Instead of:

  ```jsx
  count = 5
  ```

- React expects you to use the setter function (`setCount`).
- We'll practice this in a later lesson.

#

### Rule 3

- When state changes, React updates the UI.
- You don't manually refresh the page.

---

## Summary

```text
State

↓

Belongs to the Component

↓

Stores Changing Data

↓

Created with useState()

↓

Updated with setState Function

↓

React Re-renders

↓

UI Updates Automatically
```

---

## Mini Quiz

Try answering these without looking back:

1. What is state?
2. Why do we use state instead of a normal variable?
3. What does `useState()` do?
4. What is the purpose of `setCount`?
5. What happens after state changes?
6. Which one can change: **props** or **state**?

---

## Quick Comparison

By now you know three core React ideas:

| Concept       | Purpose                                             |
| ------------- | --------------------------------------------------- |
| **Component** | A reusable piece of UI                              |
| **Props**     | Data passed from a parent to a child                |
| **State**     | Data owned by a component that can change over time |

If you understand these three concepts, you've built the foundation that almost every React and Next.js application relies on.

---

## Today's Assignment

Don't try to memorize the syntax.

Instead, be able to explain this flow:

```text
User clicks a button

↓

State changes

↓

React notices the change

↓

The component runs again

↓

The screen shows the new value
```

If you can explain **why state exists** and how it's different from **props**, you've successfully completed today's lesson.

---

## Next Lesson (Step 8)

We'll learn **Events in React**.

We'll answer:

* What is an event?
* What are event handlers?
* How does React handle button clicks?
* How do input fields detect typing?
* How do events and state work together?

This is where your components will become interactive for the first time. From here on, you'll start seeing how React applications respond to user actions.
