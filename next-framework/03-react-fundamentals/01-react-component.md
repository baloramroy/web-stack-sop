Phase 2 — React Fundamentals

# Lesson 1 – Your First Component

## Goal of This Lesson

By the end of this lesson, you should be able to answer:

- What is React?
- What is a Component?
- Why do Components exist?
- How does Next.js use Components?
- How do you create your first Component?

Nothing more.

---

## Before We Learn Components…

**Let's understand why React was created.**

Imagine you want to build a website like Amazon.
- The page contains:

	```text
	------------------------------------
	Logo        Search      Cart
	------------------------------------

	Categories

	------------------------------------

	Product 1
	Product 2
	Product 3
	Product 4

	------------------------------------

	Footer
	```

**Now imagine you need to create 100 product cards.**
- Without React, you might copy and paste the same HTML over and over:

	```html
	<div>
			<h2>iPhone 16</h2>
			<p>$999</p>
	</div>

	<div>
			<h2>Samsung S25</h2>
			<p>$899</p>
	</div>

	<div>
			<h2>Pixel 10</h2>
			<p>$799</p>
	</div>

	...
	```

- This becomes difficult to maintain.
- Suppose tomorrow your manager says:

	> "Please add a ⭐ icon to every product card."

- Now you might have to edit hundreds of places.\
  `Not ideal.`

---

## The React Solution

- React says:

	> **Instead of repeating HTML, create reusable pieces called Components.**

- Think of a component as a **blueprint**.

	Example:

	```text
	Product Card
	```

	Instead of writing the HTML 100 times:

	```text
	Product Card

	Product Card

	Product Card

	Product Card

	Product Card
	```

- Each one can display different information while using the same structure.

---

## Real-World Analogy

- Imagine building a house.
- A house has many reusable parts:

	```text
	Door

	Window

	Chair

	Table

	Fan

	Light
	```

- You don't build a new kind of chair every time.
- You reuse the same design.
- React works the same way.
- A webpage is made of reusable building blocks.

---

## A Modern Website is Just Components

- For example, the ChatGPT interface could be broken into components like:

	```text
	Chat Page

	├── Sidebar
	│     ├── Conversation Item
	│     ├── Conversation Item
	│     └── Conversation Item
	│
	├── Header
	│
	├── Chat Area
	│     ├── User Message
	│     ├── AI Message
	│     ├── User Message
	│     └── AI Message
	│
	├── Input Box
	│
	└── Footer
	```

- Every box above can be its own component.

---

## What Is a Component?

- A component is simply:

	> **A reusable piece of UI (User Interface).**

- Examples:

	- Navbar
	- Footer
	- Login Form
	- Button
	- Product Card
	- User Profile
	- Search Box
	- Sidebar

- Each of these is a component.

---

## In Next.js

- Everything you build is made from components.
- Even this page:

	```text
	/
	```

	> is actually a React component.

- When you open:

	```text
	http://localhost:3000
	```

- Next.js loads a file named:

	```text
	page.tsx
	```

	> Inside that file is a React component.

- So when you write Next.js, you are really writing React components.

---

## Your First Component

**Here is the simplest possible React component:**

```jsx
function Welcome() {
		return <h1>Hello World</h1>;
}
```

#

**Let's understand it line by line.**

- First `welcome()` function:

	```jsx
	function Welcome() {
	```

	> This creates a JavaScript function named `Welcome`.


- Then `return` command:

	```jsx
	return
	```
	> This tells React: \
	> "This is what I want to display on the screen."

- Then `html` block:

	```jsx
	<h1>Hello World</h1>
	```
	> This tells React: \
	> This is the UI the component returns.
#

- So:

	```jsx
	function Welcome() {
			return <h1>Hello World</h1>;
	}
	```

- means:

	> Create a reusable UI block that displays **Hello World**.

---

## Visual Representation

- Like: 

	```text
	Welcome Component

			│

			▼

	+----------------------+
	|     Hello World      |
	+----------------------+
	```

---

## Components Are Like Functions

- If you already know JavaScript functions:

	```javascript
	function add(a, b) {
			return a + b;
	}
	```

- A React component follows the same idea:

	```jsx
	function Welcome() {
			return <h1>Hello</h1>;
	}
	```

- The key difference is:

	| JavaScript Function | React Component             |
	| ------------------- | --------------------------- |
	| Returns a number    | Returns UI                  |
	| Returns a string    | Returns HTML-like markup    |
	| Used for logic      | Used to build the interface |

---

## Important Rule

A component name **must start with a capital letter**.

- ✅ Correct:

	```jsx
	function Welcome() {}
	```

	```jsx
	function ProductCard() {}
	```

	```jsx
	function Navbar() {}
	```

- ❌ Incorrect:

	```jsx
	function welcome() {}
	```

> React treats lowercase names differently (as HTML elements), so using PascalCase for component names is the convention.

---

## What You Should Understand Today

Don't worry about writing code yet.

Just understand these ideas:

- A website is made of many small UI pieces.
- Each UI piece is called a **Component**.
- Components are reusable.
- A React component is just a JavaScript function that returns UI.
- Next.js applications are built by combining many React components.

---

## Mini Quiz

Try answering these without looking back:

1. Why was React created?
2. What is a Component?
3. Why are Components reusable?
4. What does a React Component return?
5. Why should a Component name start with a capital letter?
6. Is `page.tsx` in Next.js a React component?


---

### Next Lesson (Step 2)

We will learn **JSX**:

- What JSX is
- Why it looks like HTML but isn't HTML
- How JavaScript and JSX work together
- What `{}` means inside JSX

We won't cover props or state until you're comfortable with JSX. One concept at a time.

---