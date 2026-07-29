**Phase 2 – React Fundamentals**

# Lesson 2 – Understanding JSX

## Goal of This Lesson

By the end of this lesson, you should be able to answer:

* What is JSX?
* Why does JSX look like HTML?
* Is JSX actually HTML?
* Why does React use JSX?
* What does `{}` mean inside JSX?

That's all.

We won't discuss props, state, events, or hooks today.

---

## Before JSX

Imagine you want to create a heading using JavaScript.

Without React, you might write:

```javascript
const heading = document.createElement("h1");
heading.textContent = "Hello World";

document.body.appendChild(heading);
```

Let's understand what is happening:

```
Create an <h1>

↓

Set its text

↓

Add it to the page
```

Even for a simple heading, that's already three steps.

Now imagine building this:

```
-----------------------------------

Logo

Navigation

Search Box

Product List

Sidebar

Footer

-----------------------------------
```

Using only `document.createElement()` would become long, repetitive, and difficult to read.

React wanted a simpler way.

---

## The React Solution

Instead of writing:

```javascript
document.createElement("h1");
```

React lets you write:

```jsx
<h1>Hello World</h1>
```

Much cleaner.

Much easier to read.

---

## What is JSX?

JSX stands for:

> **JavaScript XML**

Don't let the name confuse you.

Today, remember this simple definition:

> **JSX is a special syntax that lets us write UI using HTML-like code inside JavaScript.**

Notice the words **HTML-like**.

Not HTML.

---

## Why Does JSX Look Like HTML?

Consider this:

```html
<h1>Hello</h1>
```

Looks exactly like HTML.

Now look at this:

```jsx
<h1>Hello</h1>
```

Looks the same.

But React treats it differently.

---

## JSX is NOT HTML

This is one of the most important things to remember.

Although JSX looks like HTML, it is **not** HTML.

It is JavaScript syntax.

Before your application runs, Next.js transforms JSX into regular JavaScript that React understands.

You don't need to know the transformation details yet. Just remember:

```
You write JSX

↓

Next.js compiles it

↓

React receives JavaScript

↓

Browser displays HTML
```

---

## Visual Flow

```
You

↓

Write JSX

↓

Next.js Compiler

↓

React

↓

Browser

↓

HTML appears
```

The browser never sees JSX directly.

---

## Example

Suppose you write:

```jsx
<h1>Hello World</h1>
```

You see:

```
Heading
```

React sees something completely different after compilation.

You don't have to memorize what it becomes.

Just know:

```
JSX

↓

JavaScript

↓

Browser
```

---

## JSX Can Contain HTML-Like Elements

Example:

```jsx
<div>
    <h1>Welcome</h1>

    <p>This is my website.</p>
</div>
```

It looks like HTML.

But it is JSX.

---

## Why Not Just Write HTML?

Because React needs JavaScript.

Suppose you have a user's name.

```javascript
const name = "Baloram";
```

How do you display it?

Traditional HTML cannot read JavaScript variables directly.

React solves this using `{}`.

---

## Curly Braces `{}`

This is probably the most important concept in today's lesson.

Whenever React sees:

```jsx
{}
```

it says:

> "Evaluate the JavaScript expression inside."

Example:

```javascript
const name = "Baloram";
```

Now:

```jsx
<h1>{name}</h1>
```

Result:

```
Baloram
```

#

Another example:

```javascript
const age = 30;
```

```jsx
<p>Age: {age}</p>
```

Output:

```
Age: 30
```

---

## Expressions Inside `{}`

You can even perform calculations.

```jsx
<h1>{5 + 10}</h1>
```

Output:

```
15
```

#

```jsx
<h1>{"Hello " + "World"}</h1>
```

Output:

```
Hello World
```

#

```jsx
<h1>{10 * 20}</h1>
```

Output:

```
200
```

---

## JSX Without `{}`

```jsx
<h1>name</h1>
```

Output:

```
name
```

Because React treats it as plain text.

---

## JSX With `{}`

```jsx
const name = "Baloram";

<h1>{name}</h1>
```

Output:

```
Baloram
```

React evaluates the variable.

---

## A Simple Example

```jsx
const city = "Dhaka";

function Welcome() {
    return (
        <div>
            <h1>Hello</h1>

            <p>City: {city}</p>
        </div>
    );
}
```

You don't need to understand every part yet.

Just notice:

```
HTML-like structure

+

JavaScript variable

=

JSX
```

---

## Mental Model

Think of JSX as a bridge.

```
JavaScript

        +

HTML-like UI

        ↓

       JSX
```

It allows you to combine JavaScript logic with the structure of your user interface.

#

## Important Rules for Today

### Rule 1

JSX looks like HTML.

But it is **not** HTML.

#

### Rule 2

JavaScript goes inside:

```jsx
{}
```

#

### Rule 3

Anything outside `{}` is treated as plain text.

Example:

```jsx
<h1>Hello</h1>
```

#

### Rule 4

Anything inside `{}` is treated as JavaScript.

Example:

```jsx
<h1>{5 + 5}</h1>
```

Result:

```
10
```

---

## Summary

```
JSX

↓

HTML-like syntax

↓

Lives inside JavaScript

↓

Compiled by Next.js

↓

Rendered by React

↓

Displayed as HTML in the browser
```

---

## Mini Quiz

Try answering these without looking back:

1. What does JSX stand for?
2. Is JSX the same as HTML?
3. Why was JSX created?
4. Does the browser understand JSX directly?
5. What do `{}` mean in JSX?
6. What is the output of:

```jsx
const name = "Alex";

<h1>{name}</h1>
```

7. What is the output of:

```jsx
<h1>{100 / 4}</h1>
```

---

## Today's Assignment

Don't write any code yet.

Your goal is to be able to explain this flow in your own words:

```
JavaScript
      +
HTML-like syntax
      ↓
     JSX
      ↓
Next.js compiles JSX
      ↓
React processes it
      ↓
Browser displays HTML
```

If you understand that flow and why `{}` are used, you've completed today's lesson.

---

## Next Lesson

We'll learn **Props**—one of the most important ideas in React.

We'll answer:

* What are props?
* Why do components need props?
* How does one component send data to another?
* Why are props called "properties"?
* How do props make components reusable?

We still won't introduce state or hooks. We'll continue building one concept at a time.
