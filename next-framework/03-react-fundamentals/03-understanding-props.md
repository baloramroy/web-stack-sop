**Phase 2 – React Fundamentals**

# Lesson 3 – Understanding Props

## Goal of This Lesson

By the end of this lesson, you should be able to answer:

* What are props?
* Why do components need props?
* What problem do props solve?
* How does one component send data to another?
* Why are props called "properties"?
* Why do props make components reusable?

That's all.

We won't discuss `useState`, events, or hooks today.

---

## Before Learning Props...

Let's imagine you're building an e-commerce website.

You already created a `ProductCard` component.

```text
+----------------------+
|     Product Card     |
+----------------------+
```

Now your website has three products:

```text
iPhone 16

Galaxy S25

Pixel 10
```

Without props, you might create three separate components:

```jsx
function IPhoneCard() {
    return <h2>iPhone 16</h2>;
}

function GalaxyCard() {
    return <h2>Galaxy S25</h2>;
}

function PixelCard() {
    return <h2>Pixel 10</h2>;
}
```

---

## What's Wrong With This?

All three components are almost identical.

Only the product name changes.

Imagine you have **500 products**.

Would you create:

```text
Product1Card

Product2Card

Product3Card

...

Product500Card
```

Of course not.

There must be a better way.

---

## The React Solution

React says:

> "Create **one** component, and pass different information to it."

That information is called **props**.

---

## What Are Props?

Props is short for:

> **Properties**

Think of props as **information you give to a component**.

A simple definition:

> **Props are values passed from one component to another.**

---

## Real-World Analogy 1: A Coffee Cup

Imagine a coffee shop.

The shop uses the same type of cup every time.

```text
☕ Cup
```

The cup (the component) is always the same.

But each customer orders something different:

```text
Cup → Coffee

Cup → Tea

Cup → Hot Chocolate
```

The **cup** doesn't change.

Only **what goes inside it** changes.

A React component works the same way.

---

## Real-World Analogy 2: A Name Badge

Imagine you're organizing a conference.

You have one badge design:

```text
----------------
Name:
Role:
----------------
```

Now you print badges for different people.

```text
----------------
Name: Alice
Role: Speaker
----------------
```

```text
----------------
Name: Bob
Role: Guest
----------------
```

```text
----------------
Name: Carol
Role: Organizer
----------------
```

The badge design never changes.

Only the values change.

Those values are like **props**.

---

## How Props Work

Imagine two components.

```text
App

↓

ProductCard
```

The parent component (`App`) sends data to the child component (`ProductCard`).

```text
App

    sends

name = "iPhone"

↓

ProductCard
```

The child receives the data and displays it.

---

## Your First Props Example

Parent component:

```jsx
<ProductCard name="iPhone 16" />
```

Let's read this like English:

> "Create a `ProductCard` and give it a property called `name` with the value `iPhone 16`."

---

Child component:

```jsx
function ProductCard(props) {
    return <h2>{props.name}</h2>;
}
```

Notice two things:

* The parent **passes** data.
* The child **receives** data.

---

## Visual Flow

```text
Parent Component

        │
        │  name = "iPhone 16"
        ▼

Child Component

        │
        ▼

Displays:

iPhone 16
```

---

## Reusing the Same Component

Now the parent can use the same component multiple times.

```jsx
<ProductCard name="iPhone 16" />

<ProductCard name="Galaxy S25" />

<ProductCard name="Pixel 10" />
```

React creates three product cards.

Each one receives different props.

The component stays exactly the same.

---

## Another Example

Imagine a greeting component.

```jsx
<Greeting name="Alice" />

<Greeting name="Bob" />

<Greeting name="Charlie" />
```

The same component can greet different people.

Without props, you'd need a separate component for every person.

---

## Why Are They Called "Properties"?

Think about a car.

A car has properties:

```text
Color

Brand

Model

Year
```

Example:

```text
Brand: Toyota

Color: White

Year: 2025
```

Those describe the car.

A React component also has properties.

For example:

```jsx
<Button text="Save" color="green" />
```

The button has two properties:

```text
text

color
```

These properties are called **props**.

---

## Props Are Read-Only

One important rule:

A component **receives** props.

It should **not change them**.

Think of receiving a sealed letter.

You can read it.

You shouldn't rewrite its contents.

For now, remember:

> Props are read-only.

Later, when we learn state, you'll understand why.

---

## Parent and Child

This relationship is very important.

```text
Parent Component

↓

Child Component
```

The parent sends props down to the child.

Data flows in one direction:

```text
Parent

↓

Child
```

This is called **one-way data flow**.

We'll revisit this idea many times as you learn React.

---

## Mental Model

Think of a component as a machine.

```text
           Props
             │
             ▼

     +----------------+
     |  Component      |
     +----------------+

             │
             ▼

           UI
```

The component takes input (props) and produces output (UI).

---

## Summary

```text
Props

↓

Short for Properties

↓

Passed from Parent

↓

Received by Child

↓

Read-only

↓

Make Components Reusable
```

---

## Mini Quiz

Try answering these without looking back:

1. What does **props** stand for?
2. Why do we use props?
3. Which component sends props?
4. Which component receives props?
5. Can a child component modify its props?
6. Why are props important for reusable components?

---

## Today's Assignment

Don't focus on memorizing the syntax.

Instead, make sure you can explain this flow:

```text
Parent Component

      │

Sends Data (Props)

      │

      ▼

Child Component

      │

Uses the Data

      │

      ▼

Displays Different UI
```

If you understand that idea, you've completed today's lesson.

---

## Next Lesson

We'll learn about **State (`useState`)**.

We'll answer:

* What is state?
* Why do we need state if we already have props?
* What's the difference between props and state?
* Why does changing state update the UI automatically?

This is one of the biggest milestones in learning React, so we'll take it slowly and build on everything you've learned so far.
