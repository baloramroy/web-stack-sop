
# Lesson 2: Understanding The Project Structure

## Objective

By the end, you should be able to look at a Next.js project and explain **what every important file and folder is for**. You don't need to know every line of code yet—just the purpose of each part.

---

## First, Create a Mental Model

- Think of a Next.js project like a company.

  ```
  Next.js Project
  │
  ├── Management Files
  ├── Application Code
  ├── Static Assets
  ├── Dependencies
  └── Configuration
  ```

>[!NOTE]
*Each folder has a specific job.* \
*Let's learn them one by one.*

---

## Project Structure

- After creating a new project, you'll see something similar to this:

  ```text
  my-first-next-app/
  │
  ├── node_modules/
  ├── public/
  ├── src/
  │   └── app/
  │       ├── favicon.ico
  │       ├── globals.css
  │       ├── layout.tsx
  │       └── page.tsx
  │
  ├── package.json
  ├── package-lock.json
  ├── next.config.ts
  ├── tsconfig.json
  ├── eslint.config.mjs
  ├── .gitignore
  └── README.md
  ```

- Don't panic.
- We're going to learn **only one item at a time.**

---

##  `package.json`

This is one of the most **important** files. Think of it as the **identity card** of your project.

- It tells Node.js:

  * What is the project name?
  * Which packages does it use?
  * How do we start the project?
  * How do we build the project?

- Example:

  ```json
  {
    "name": "my-first-next-app",
    "version": "0.1.0",
    "scripts": {
      "dev": "next dev",
      "build": "next build",
      "start": "next start"
    }
  }
  ```

- **The most important section**

  ```json
  "scripts": {
    "dev": "next dev"
  }
  ```

- When you type:

  ```bash
  npm run dev
  ```

- npm looks inside `package.json`.

  ```
  npm run dev
          │
          ▼
  package.json
          │
          ▼
  "dev": "next dev"
          │
          ▼
  Start Next.js
  ```

> **Remember:** \
**npm run dev** doesn't magically know what to do. \
It simply **executes** the command defined in **package.json**.

---

## `package-lock.json`

Beginners often **ignore** this file. \
Its purpose is to **lock the exact versions** of every installed package.

- Imagine **two developers** working on the **same project**.

- Without `package-lock.json`:

  ```
  Developer A
  React 19.1

  Developer B
  React 19.3
  ```

- They might get **different behavior**.

- With `package-lock.json`:

  ```
  Everyone installs exactly the same versions.
  ```

> This keeps projects consistent.

---

## `node_modules/`

This folder contains all the **packages** your project **depends** on.

- For example:

  ```
  React

  Next.js

  TypeScript

  ESLint

  Tailwind CSS

  ...and many more
  ```

  > You didn't write this code.

- npm downloaded it for you.

  ```
  npm install
          │
          ▼
  Downloads Packages
          │
          ▼
  node_modules/
  ```

### Important Rule

- **Never edit anything inside `node_modules`.**

> It's managed automatically.

---

## `public/`

This folder stores **static files**.

- Examples:

  ```
  logo.png

  banner.jpg

  favicon.ico

  robots.txt
  ```

These files are **served directly** to the **browser**.

- If you place:

  ```
  public/logo.png
  ```

- you can access it like this:

  ```
  http://localhost:3000/logo.png
  ```

> Think of `public` as a storage area for files that don't need processing.

---

## `src/`

This is where **your application code** lives.

- Think of it as the heart of your project.

  ```
  src/
  ```

- Contains the code you write:

  * Components
  * Pages
  * Styles
  * Logic
  * API routes (later)

> Everything important will happen here.

---

## `app/`

This is one of the most **important folders** in modern **Next.js**.

- The `app` folder uses the **App Router**.

- Inside it, folders represent routes.

- For example:

  ```
  app/
      page.tsx
  ```

- creates:

  ```
  /
  ```

- If you create:

  ```
  app/about/page.tsx
  ```

- you automatically get:

  ```
  /about
  ```

- Think of it like this:

  ```
  Folder

  ↓

  URL
  ```

> We'll explore routing in depth later.

#

### `page.tsx`

Every route needs a `page.tsx`. This file defines **what the user sees**.

- Example:

  ```tsx
  export default function Home() {
    return <h1>Welcome</h1>;
  }
  ```

- When you visit:

  ```
  localhost:3000
  ```

- Next.js renders this component.

  ```
  Browser

  ↓

  page.tsx

  ↓

  HTML

  ↓

  Screen
  ```

#

### `layout.tsx`

- Imagine every page on your website should have:

  * A navigation bar
  * A footer

- Instead of adding them to every page, `layout.tsx` lets you define shared UI once.

  ```
  Navbar

  ↓

  Page Content

  ↓

  Footer
  ```

- Every page is displayed inside this layout.

> We'll study layouts in detail later.

#

### `globals.css`

This file contains styles that apply to the entire application.

Examples:

* Font settings
* Background color
* Global spacing
* CSS variables

Unlike CSS Modules, these styles affect the whole app.

---

## `next.config.ts`

This is Next.js's configuration file.

Later, you'll use it to configure things like:

* Image optimization
* Redirects
* Environment settings
* Experimental features

For now, just know it's the project's configuration file.

---

## `tsconfig.json`

Since we chose TypeScript during setup, this file configures the TypeScript compiler.

It tells TypeScript:

* Where your code is
* Which language features to use
* How to resolve imports

You won't need to modify it right now.

---

## `eslint.config.mjs`

This configures **ESLint**, which checks your code for **potential mistakes** and enforces coding standards.

Think of it as a helpful reviewer that points out issues before they become bugs.

---

## Putting It All Together

Here's how these pieces relate:

```text
Next.js Project
│
├── package.json            → Project information and scripts
├── package-lock.json       → Locks package versions
├── node_modules/           → Installed libraries
├── public/                 → Static files (images, icons, etc.)
├── src/                    → Your application code
│     └── app/
│          ├── layout.tsx   → Shared layout
│          ├── page.tsx     → Home page
│          └── globals.css  → Global styles
├── next.config.ts          → Next.js configuration
├── tsconfig.json           → TypeScript configuration
└── eslint.config.mjs       → ESLint configuration
```

---

## Next Lesson

Once you're comfortable with the project structure, we'll move to:

[**Lesson 3: How Next.js Actually Works**]()

