**Phase 2 – React Fundamentals**

# Lesson 6 – Rendering Lists

So far we've learned:

* ✅ Step 4 – Components
* ✅ Step 5 – JSX
* ✅ Step 6 – Props
* ✅ Step 7 – State
* ✅ Step 8 – Events

Today we'll learn another fundamental concept that you'll use almost every day.

---


## Goal of This Lesson

By the end of this lesson, you should be able to answer:

* Why do we render lists?
* Why does React use `map()`?
* How does React create multiple components from an array?
* What is the `key` prop?
* Why is `key` important?

That's all.

We won't discuss filtering, sorting, or APIs yet.

---

## Before Learning Lists...

Imagine you're building an online store.

You have these products:

```text
iPhone 16

Galaxy S25

Pixel 10

Nothing Phone 4
```

Your webpage should display:

```text
---------------------
📱 iPhone 16
---------------------

---------------------
📱 Galaxy S25
---------------------

---------------------
📱 Pixel 10
---------------------

---------------------
📱 Nothing Phone 4
---------------------
```

How would you do this?

---

## Without React Lists

You might write:

```jsx
<ProductCard name="iPhone 16" />

<ProductCard name="Galaxy S25" />

<ProductCard name="Pixel 10" />

<ProductCard name="Nothing Phone 4" />
```

This works.

But imagine you have:

```text
10 Products

100 Products

5,000 Products
```

Would you write thousands of `ProductCard` components manually?

Of course not.

---

## The Real Situation

In real applications, the products usually come as data.

Example:

```text
Products

↓

iPhone 16

Galaxy S25

Pixel 10

Nothing Phone 4
```

Instead of writing every card yourself, you want React to create them automatically.

---

## The React Solution

React says:

> "Give me the list of data, and I'll create the UI for each item."

This process is called **Rendering a List**.

---

## What is Rendering?

You've heard the word "render" several times.

A simple definition:

> **Rendering means displaying UI on the screen.**

Examples:

```text
Data

↓

React

↓

UI appears
```

---

## What is a List?

A list is simply:

> **Multiple pieces of similar data.**

Examples:

- Products

  ```text
  Phone A

  Phone B

  Phone C
  ```

- Users

  ```text
  Alice

  Bob

  Charlie
  ```

- Messages

  ```text
  Hello

  How are you?

  See you tomorrow
  ```

- Orders

  ```text
  Order #101

  Order #102

  Order #103
  ```

React displays these collections using list rendering.

---

## Real-World Analogy

Imagine a bakery.

- A customer orders:

  ```text
  10 Cookies
  ```

  The baker doesn't make ten different recipes.

- The baker uses:

  ```text
  One Recipe

  ↓

  Repeat

  ↓

  10 Cookies
  ```

React works exactly the same way.

- One component.
- Many pieces of data.
- Many UI elements.

---

## Another Analogy

Imagine a school printing report cards.

- The report card design is always the same.

  ```text
  ----------------

  Name:

  Class:

  Marks:

  ----------------
  ```

- Only the student information changes.

  ```text
  Student 1

  ↓

  Report Card
  ```

  ```text
  Student 2

  ↓

  Report Card
  ```

  ```text
  Student 3

  ↓

  Report Card
  ```

- The template stays the same.
- The data changes.

That's list rendering.

---

## Arrays

React usually renders lists from an **array**.

- Example:

  ```javascript
  const products = [
      "iPhone 16",
      "Galaxy S25",
      "Pixel 10"
  ];
  ```
- You don't need to learn arrays today.

Just understand:\
`An array is a collection of values.`

---

## Why `map()`?

- Imagine you have:

  ```text
  Apple

  Banana

  Orange
  ```

- React needs to create UI for each:

  ```text
  🍎 Apple

  🍌 Banana

  🍊 Orange
  ```

- It needs to repeat the same UI for every item.
- But JavaScript already has a method that repeats work for every item in an array.
- That method is:

  ```javascript
  map()
  ```

---

## Think of `map()` Like a Factory

Imagine a factory.

- Raw materials enter:

  ```text
  Apple

  Banana

  Orange
  ```

- The machine performs the same process on each item.

  Output:

  ```text
  Juice

  Juice

  Juice
  ```

`map()` works similarly.

- Input:

  ```text
  Data
  ```

- Output:

  ```text
  UI
  ```

---

## Visual Flow

```text
Products Array

↓

map()

↓

ProductCard

↓

ProductCard

↓

ProductCard

↓

Screen
```

---

## A Simple Example

- Imagine this array:

  ```javascript
  const names = [
      "Alice",
      "Bob",
      "Charlie"
  ];
  ```

- React uses `map()` to create:

  ```text
  Hello Alice

  Hello Bob

  Hello Charlie
  ```

Notice something.

- You didn't write:

  ```jsx
  <h1>Hello Alice</h1>

  <h1>Hello Bob</h1>

  <h1>Hello Charlie</h1>
  ```

React generated them from the data.

---

## What is `key`?

- Now imagine these products:

  ```text
  1. iPhone

  2. Galaxy

  3. Pixel
  ```

Tomorrow the owner removes Galaxy.

- Now the list becomes on UI:

  ```text
  1. iPhone

  2. Pixel
  ```

- React has to figure out in UI:

  ```text
  Which item disappeared?

  Which item stayed?

  Which item moved?
  ```

- Without extra information, React has to guess.
- That's inefficient.

---

## React's Solution

React asks:

> "Can you give every item a unique identity?"

That identity is called:

```text
key
```

---

## Real-World Analogy

Imagine a classroom.
- Every student has:

  ```text
  Name

  Roll Number
  ```

- The teacher identifies students by their **roll number**, not just by where they're sitting.
- Even if Alice moves to another seat, her roll number is still the same.
- React treats `key` the same way.
- It uses the key to identify each item.

---

## Visual Example

Without keys:

```text
Apple

Banana

Orange
```

React only sees positions.

#

With keys:

```text
ID 101 → Apple

ID 102 → Banana

ID 103 → Orange
```

Now React knows exactly which item is which.

---

## Why is `key` Important?

- Suppose your shopping cart contains:

  ```text
  Laptop

  Mouse

  Keyboard
  ```

- You remove:

  ```text
  Mouse
  ```

- Without keys: \
  React compares everything again.

- With keys: \
  - React immediately knows:
  - "Only the item with ID 102 was removed."

> That makes updates much faster and more reliable.

---

## Mental Model

```text
Array

↓

map()

↓

Create UI

↓

Each Item Gets a Key

↓

React Tracks Every Item

↓

Screen Updates Efficiently
```

---

## How Everything Fits Together

Let's connect what you've learned so far.

```text
Array of Data

↓

map()

↓

Components

↓

Rendered UI

↓

User Clicks

↓

Events

↓

State Changes

↓

React Updates Only the Changed Items
```

This is how many real-world applications display products, messages, notifications, comments, users, and much more.

---

## Important Rules

### Rule 1

Lists are usually created from arrays.

#

### Rule 2

React commonly uses `map()` to create UI from arrays.

#

### Rule 3

Every item in a rendered list should have a unique `key`.

#

### Rule 4

The `key` should be unique and stable (for example, a database ID), not something that changes every render.

We'll discuss good and bad keys later.

---

## Summary

```text
Array

↓

map()

↓

Components

↓

key

↓

React Tracks Items

↓

Efficient UI Updates
```

---

## Mini Quiz

Try answering these without looking back.

### 1.

What does **rendering a list** mean?

#

### 2.

Why does React use `map()`?

#

### 3.

Where does the list usually come from?

#

### 4.

What is the purpose of the `key` prop?

#

### 5.

Why shouldn't React rely only on the item's position in the list?

#

### 6.

Complete this flow:

```text
Array

↓

?

↓

Components

↓

?

↓

React Updates UI
```

---

## What You've Learned So Far

| Step | Concept    | Purpose                            |
| ---- | ---------- | ---------------------------------- |
| 4    | Components | Build reusable UI pieces           |
| 5    | JSX        | Describe UI using HTML-like syntax |
| 6    | Props      | Pass data between components       |
| 7    | State      | Store changing data                |
| 8    | Events     | Respond to user actions            |
| 9    | Lists      | Display many items from data       |

Notice how the concepts are building on one another. Each lesson adds one new piece to the puzzle rather than introducing something completely unrelated.

---

## Today's Assignment

Make sure you can explain this flow:

```text
Data (Array)

↓

React uses map()

↓

Creates Components

↓

Each Component gets a unique key

↓

React renders the list

↓

Later, React uses the keys to update only the items that changed
```

If you understand **why `map()` exists** and **why React needs `key`**, you've completed today's lesson.

---

## Next Lesson

We'll learn **Conditional Rendering**.

You'll answer questions like:

* How do we show something only when a condition is true?
* How do we hide UI?
* What are `if`, the ternary operator (`? :`), and `&&` in React?
* How do real applications decide what to display?

This is the final core React concept we'll cover before we start putting everything together in practical Next.js pages.
