**Phase 2 – React Fundamentals**

# Lesson 5 – Understanding Events

So far you've learned:

* ✅ Step 4 – Components
* ✅ Step 5 – JSX
* ✅ Step 6 – Props
* ✅ Step 7 – State

Now it's time to connect everything together.

---

### Goal of This Lesson

By the end of this lesson, you should be able to answer:

* What is an event?
* What is an event handler?
* How does React know when a user clicks a button?
* How do events and state work together?
* Why are events important?

That's all.

We won't cover forms or `useEffect` today.

---

# Before Learning Events...

Imagine you visit an online shopping website.

You click:

```text
Add to Cart
```

Immediately:

```text
Cart (1)
```

appears.

How did the website know you clicked the button?

Because the button generated an **event**.

---

# What is an Event?

An event is simply:

> **Something that happens in the application.**

Think of an event as a signal that tells React:

> "The user just did something."

---

# Examples of Events

A user can perform many actions.

```text
Click a button

↓

Type in a textbox

↓

Move the mouse

↓

Press a key

↓

Submit a form

↓

Scroll the page
```

Every one of these actions is an **event**.

---

# Real-World Analogy

Imagine your house has a doorbell.

Someone presses it.

```text
Person

↓

Presses Doorbell

↓

Bell Rings

↓

You Open the Door
```

The button press is the **event**.

The bell ringing is the **response**.

React works exactly the same way.

---

# Another Analogy

Imagine you're in a classroom.

The teacher asks:

> "Raise your hand if you know the answer."

A student raises a hand.

```text
Student raises hand

↓

Teacher notices

↓

Teacher responds
```

The raised hand is an event.

The teacher's response is like React running your code.

---

# What is an Event Handler?

If an event is **what happened**, then an **event handler** is:

> **The function that React runs when the event happens.**

For example:

```text
Button Click

↓

Run a Function

↓

Update Something
```

That function is called the **event handler**.

---

# Your First Event

Imagine this button:

```jsx
<button>Click Me</button>
```

Right now it doesn't do anything.

It's just a button.

---

Now imagine:

```jsx
<button onClick={sayHello}>
    Click Me
</button>
```

Read it like English:

> "When this button is clicked, run `sayHello`."

The important part is:

```jsx
onClick
```

This is a React event.

---

# Visual Flow

```text
User

↓

Clicks Button

↓

onClick Event

↓

Event Handler Runs

↓

React Does Something
```

---

# Common React Events

React has many built-in events.

Here are a few you'll use frequently:

| Event          | When it Happens         |
| -------------- | ----------------------- |
| `onClick`      | Button is clicked       |
| `onChange`     | Input value changes     |
| `onSubmit`     | Form is submitted       |
| `onKeyDown`    | Key is pressed          |
| `onMouseEnter` | Mouse enters an element |
| `onMouseLeave` | Mouse leaves an element |

Don't try to memorize all of them today.

Just remember:

React provides events for user interactions.

---

# Events by Themselves

Imagine:

```text
Click Button

↓

Show an alert
```

Simple.

---

But React becomes powerful when you combine:

```text
Event

+

State
```

---

# Events + State

Suppose you have:

```text
Count: 0
```

The user clicks:

```text
Increment
```

Flow:

```text
User Clicks Button

↓

onClick Event

↓

Event Handler Runs

↓

State Changes

↓

React Re-renders

↓

Count: 1
```

Notice something important.

The **event** does not update the screen directly.

Instead:

```text
Event

↓

Changes State

↓

React Updates UI
```

This is one of React's biggest ideas.

---

# Another Example

Imagine a light switch.

Initially:

```text
💡 OFF
```

User clicks.

```text
💡 ON
```

User clicks again.

```text
💡 OFF
```

What's happening?

```text
Click Event

↓

State Changes

↓

UI Changes
```

---

# Login Form Example

Imagine a login page.

The user types:

```text
Username

Password
```

Every key press generates an event.

```text
Keyboard Event

↓

Input Value Changes

↓

State Updates

↓

Screen Shows New Value
```

Without events, React wouldn't know the user typed anything.

---

# Shopping Cart Example

Imagine this button.

```text
Add to Cart
```

User clicks.

```text
Cart: 0

↓

Cart: 1
```

Flow:

```text
Click Event

↓

Update Cart State

↓

React Updates Cart Icon
```

---

# Mental Model

Whenever a user interacts with your application:

```text
User Action

↓

Event Occurs

↓

Event Handler Runs

↓

State Changes

↓

React Re-renders

↓

Updated UI
```

Almost every React application follows this pattern.

---

# How Everything You've Learned Fits Together

Let's connect all the concepts.

Imagine a simple counter app.

```text
Counter Component
```

Inside the component:

```text
State

↓

count = 0
```

On the screen:

```text
Count: 0

[ + ]
```

User clicks:

```text
+

↓

onClick Event

↓

Event Handler

↓

State Changes

↓

React Re-renders

↓

Count: 1
```

Notice how all the concepts work together.

---

# The React Building Blocks

Here's the complete picture so far.

```text
Component

↓

Contains

↓

JSX

↓

Receives Props

↓

Stores State

↓

Handles Events

↓

Updates UI
```

This is the foundation of React.

---

# Important Rules

### Rule 1

Events happen because of user actions.

---

### Rule 2

Events trigger event handlers.

---

### Rule 3

Event handlers often update state.

---

### Rule 4

Changing state causes React to re-render the component.

---

# Summary

```text
User Action

↓

Event

↓

Event Handler

↓

State Changes

↓

React Re-renders

↓

Updated UI
```

If you understand this flow, you understand how React applications become interactive.

---

# Mini Quiz

Try answering these without looking back.

### 1.

What is an event?

---

### 2.

What is an event handler?

---

### 3.

Which event runs when a button is clicked?

---

### 4.

Does an event update the UI directly?

---

### 5.

What usually happens after an event handler changes state?

---

### 6.

Complete this flow:

```text
User Click

↓

?

↓

?

↓

React Re-renders

↓

Updated UI
```

---

# What You've Learned So Far

Let's pause for a moment and see how the pieces fit together:

| Lesson | What You Learned                                                                |
| ------ | ------------------------------------------------------------------------------- |
| Step 4 | Components are reusable building blocks of the UI.                              |
| Step 5 | JSX lets you describe UI using HTML-like syntax inside JavaScript.              |
| Step 6 | Props allow parent components to pass data to child components.                 |
| Step 7 | State stores data that belongs to a component and can change.                   |
| Step 8 | Events let users interact with the application and often trigger state changes. |

At this point, you understand the **core mental model of React**. These five concepts appear in almost every React and Next.js application you'll build.

---

# Today's Assignment

Make sure you can explain this entire flow in your own words:

```text
User clicks a button

↓

React receives an event

↓

An event handler runs

↓

The handler updates state

↓

React re-renders the component

↓

The browser shows the updated UI
```

If you can explain that without looking at the notes, you've completed today's lesson.

---

## Next Lesson

We'll learn **Rendering Lists**.

You'll discover:

* Why React uses `map()`
* How to display multiple items from an array
* What the `key` prop is and why it's important
* How React efficiently updates lists

This is the next essential building block before we start creating more realistic user interfaces.
