# Lesson 1: Understanding Node.js, npm, and npx

## Learning Objective

By the end of this lesson, we will be able to answer:

* What is Node.js?
* What is npm?
* Why do we need Node.js for Next.js?
* What does `create-next-app` do?
* How do we run a Next.js application?

---

## Before We Install Anything

Many beginners think they only install Node.js, but the installer actually gives you three important tools:

```
Node.js Runtime
       │
       ├── node
       ├── npm
       └── npx
```

Each has a different purpose.

---

## 1. What is Node.js?

Normally, JavaScript(a programming language) runs only inside a web browser.

- For example:

  ```javascript
  console.log("Hello");
  ```

This works in Chrome, Firefox, or Edge because they have a JavaScript engine.

**Question:** \
What if you want to run JavaScript directly on your computer without a browser?

That's exactly what **Node.js** does.

Node.js is a JavaScript runtime that lets you execute JavaScript on your operating system.

- For example, create a file named `test.js`:

  ```javascript
  console.log("Hello from Node.js");
  ```

- Run it with:

  ```bash
  node test.js
  ```

- Output:

  ```
  Hello from Node.js
  ```

Here, the `node` command runs your JavaScript file.

#

### Why does Next.js need Node.js?

When you create a Next.js project, you're not just opening an HTML file.

- **Next.js needs to:**

  * Compile your code
  * Bundle your files
  * Start a development server
  * Watch for changes
  * Install packages

  Those tasks are handled by Node.js.

- **Think of it this way:**

  ```
  Your Code
        ↓
  Next.js
        ↓
  Node.js
        ↓
  Operating System
  ```

>Without Node.js, Next.js cannot run.

---

## 2. What is npm?

When you build applications, you don't write everything yourself. You use libraries created by other developers.

Examples include:

* React
* Next.js
* Axios
* Express
* Tailwind CSS

These libraries are called **packages**.

`npm` stands for **Node Package Manager**.

It helps you:

* Install packages
* Update packages
* Remove packages
* Manage project dependencies

Example:

```bash
npm install react
```

This downloads React into your project.

---

## 3. What is npx?

>This is the part that often confuses beginners.

  Suppose you want to create a new Next.js project.

- One way would be:

  ```bash
  npm install -g create-next-app
  ```

- Then:

  ```bash
  create-next-app my-app
  ```

This installs `create-next-app` globally on your computer.

### NPX

Instead, `npx` lets you run a package **without installing it globally**.

Example:

  ```bash
  npx create-next-app@latest my-app
  ```

Here's what happens:

1. `npx` downloads the latest `create-next-app` package (if needed).
2. It runs the tool.
3. It creates your project.
4. It exits. You don't have to manage a global installation.

That's why you'll see `npx` used frequently in modern JavaScript development.

---

## Relationship Between Them

```
                 Node.js
                    │
         ┌──────────┴──────────┐
         │                     │
       node                  npm
                                │
                               npx
```

* **Node.js** provides the runtime.
* **node** runs JavaScript files.
* **npm** manages packages.
* **npx** runs package executables without a global install.


---

## What Happens When You Create a Next.js Project?

- When you run:

  ```bash
  npx create-next-app@latest my-first-next-app
  ```

- The process looks like this:

  ```
  You
  │
  │
  ▼
  npx
  │
  ▼
  Downloads create-next-app (if needed)
  │
  ▼
  Runs the project generator
  │
  ▼
  Creates your project folder
  │
  ▼
  Installs dependencies using npm
  │
  ▼
  Your Next.js project is ready
  ```

---

## What is the Development Server?

- When you run:

  ```bash
  npm run dev
  ```

  >Node.js starts a local web server.

- For example:

  ```
  http://localhost:3000
  ```

  >Now your browser can access your application.

- The flow looks like this:

  ```
  You
      ↓
  npm run dev
      ↓
  Node.js
      ↓
  Next.js Development Server
      ↓
  localhost:3000
      ↓
  Browser
  ```

This server automatically reloads your application whenever you save a file, making development much faster.


---

## Key Takeaways

| Command | Purpose                                                |
| ------- | ------------------------------------------------------ |
| `node`  | Runs JavaScript files                                  |
| `npm`   | Installs and manages packages                          |
| `npx`   | Runs package executables without a global installation |

---

