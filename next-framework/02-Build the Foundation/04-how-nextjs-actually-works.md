Phase 1 — Build the Foundation

# Lesson 4: How Next.js Actually Works

## Learning Objective

By the end of this lesson, you'll be able to answer:

* What happens after I type `http://localhost:3000`?
* What does `npm run dev` actually do?
* What is the Next.js development server?
* How does Next.js find `page.tsx`?
* Where does React fit into Next.js?
* How does HTML reach the browser?

If you understand this flow, you've completed the lesson.

---

## Before We Start

Let's clear up one common misconception.

- Many beginners think:

	```text
	Browser
		↓
	React
		↓
	Browser
	```

  >That's **not** how a Next.js application works.

- Instead, the flow is more like this:

	```text
	Browser
		↓
	Next.js Server
		↓
	React
		↓
	HTML
		↓
	Browser
	```

- Notice something important.\
	*"The browser does **not** talk directly to React."*\
	*"React is used **inside Next.js**"*.

---

## What Happens When You Run `npm run dev`?

- Suppose you type:

	```bash
	npm run dev
	```

- Does npm itself start your website?
	
	```
	**No.**
	```

- Remember from Lesson 3:

	```json
	{
		"scripts": {
			"dev": "next dev"
		}
	}
	```

- The command works like this:

	```text
	You

	↓

	npm run dev

	↓

	package.json

	↓

	next dev

	↓

	Node.js

	↓

	Starts Next.js Development Server
	```

	> So the real work is done by **`next dev`**, which runs using **Node.js**.

---

## The Development Server Starts

- After a few seconds, you'll see something like:

	```text
	▲ Next.js 16.x

	Ready in 1.8s

	Local:
	http://localhost:3000
	```

  * Now something new exists.
  * A **web server**.

- Think of it like a waiter in a restaurant.

	```text
	Customer

	↓

	Waiter

	↓

	Kitchen

	↓

	Waiter

	↓

	Customer
	```

  * The waiter **receives requests**.
  * The waiter does **not cook**.

- Similarly:

	```text
	Browser

	↓

	Next.js Server

	↓

	React

	↓

	Next.js Server

	↓

	Browser
	```

	> The server coordinates everything.

---

## You Open the Browser

- Now you visit:

	```text
	http://localhost:3000
	```

- The browser sends a request.

	```text
	Browser

	↓

	"Give me the home page."
	```

	-	Who receives it?
	-	Not React.
	-	Not `page.tsx`.

- The request first reaches:

	```text
	Next.js Development Server
	```

---

## Next.js Receives the Request

- Now Next.js asks itself:

	```
	"The user requested `/`."
	```

- Which page should I show?

	```
	It starts looking inside the **App Router**.
	```

---

## The App Router Looks for the Route

- **Remember:**\
	`Folders create routes.`

- Suppose your project looks like this:

	```text
	src/
	└── app/
			├── page.tsx
			├── about/
			│   └── page.tsx
			└── contact/
					└── page.tsx
	```

#

### Now imagine three requests.

- **Request 1**

	```text
	/
	```

	Next.js finds

	```text
	app/page.tsx
	```


- **Request 2**

	```text
	/about
	```

	Next.js finds

	```text
	app/about/page.tsx
	```


- **Request 3**

	```text
	/contact
	```

	Next.js finds

	```text
	app/contact/page.tsx
	```

> The App Router is simply matching the requested URL to the correct `page.tsx`.

---

## Next.js Executes the React Component

- Let's say `app/page.tsx` contains:

	```tsx
	export default function Home() {
		return <h1>Hello Next.js</h1>;
	}
	```

  * Notice something.
  * This is **just a JavaScript function**.

- Next.js executes it.

	```text
	Home()

	↓

	Returns JSX
	```

  * The function does **not** directly create HTML.
  * It returns **JSX**.

---

## React Processes the JSX

Now React takes over.

- React sees:

	```tsx
	<h1>Hello Next.js</h1>
	```

	* React understands JSX.
	* It transforms that JSX into HTML.

- Conceptually:

	```text
	JSX

	↓

	React

	↓

	HTML
	```

- For example:

	```html
	<h1>Hello Next.js</h1>
	```

This HTML is what browsers understand.

> **A small note:** Internally, React first creates its own element representation before producing HTML. For now, it's enough to think of it as "React turns JSX into the HTML the browser can display."

---

## Next.js Sends the Response

Now **Next.js** has the **HTML**.

- It sends it back.

	```text
	Next.js Server

	↓

	HTML

	↓

	Browser
	```

---

## The Browser Displays the Page

- Finally:

	```text
	Browser

	↓

	Reads HTML

	↓

	Displays the page
	```

- You now see:

	```
	Hello Next.js
	```

- on your screen.

---

## The Complete Flow

- Let's put everything together.

	```text
	You

	↓

	Open Browser

	↓

	http://localhost:3000

	↓

	Browser sends request

	↓

	Next.js Development Server receives request

	↓

	App Router looks for matching route

	↓

	Finds app/page.tsx

	↓

	Executes the React component

	↓

	Component returns JSX

	↓

	React processes the JSX

	↓

	Next.js sends HTML

	↓

	Browser receives HTML

	↓

	Browser renders the page
	```

	> This is the complete request flow.

---

## Where Does Node.js Fit?

**Many beginners ask:**

> "Where is Node.js in all this?"

**Remember:**

- Node.js is running the Next.js server.

	```text
	Operating System

	↓

	Node.js Runtime

	↓

	Next.js Development Server

	↓

	React

	↓

	HTML
	```

- Without Node.js:

	* No development server
	* No routing
	* No compilation
	* No React execution on the server

---

## A Restaurant Analogy

- Sometimes analogies make the architecture easier to remember.

	```text
	Customer
					↓
	Browser

	Waiter
					↓
	Next.js Server

	Chef
					↓
	React

	Meal
					↓
	HTML

	Customer Eats
					↓
	Browser Displays Page
	```

- Notice the roles:

	* **Browser** = Customer placing an order.
	* **Next.js Server** = Waiter receiving the order and bringing back the result.
	* **React** = Chef preparing the page.
	* **HTML** = The finished meal delivered to the customer.

---

## A Peek Into the Future

Right now, our page is very simple.

- Later in the course, the flow will become richer:

	```text
	Browser
				↓
	Next.js Server
				↓
	Authentication Check
				↓
	Database Query
				↓
	API Call
				↓
	React Components
				↓
	HTML
				↓
	Browser
	```

You'll learn each new step one at a time, but the core request flow you've learned today remains the backbone of every Next.js application.


---

## One Small Clarification

In this lesson, I simplified one part by saying **"React turns JSX into HTML."** That's the right mental model for where you are now.

Later, when we study **Server Components**, **Client Components**, **hydration**, and **rendering strategies**, we'll refine that explanation and see exactly how React and Next.js collaborate. For now, the simplified model is the best foundation before adding those advanced details.

---
