# Lesson 1: Create Your First Next.js Project

## Objective

By the end of this lesson, we will:

* Create our first Next.js project
* Understand every question asked by the project generator
* Know what is happening behind the scenes
* Successfully run our application

---

## Step 1: Open a Terminal

### Windows

Open one of these:

* Command Prompt
* PowerShell
* Windows Terminal (Recommended)

Verify Node is installed:

```powershell
node -v
npm -v
npx -v
```

#

### RHEL

Open a terminal.

Verify:

```bash
node -v
npm -v
npx -v
```

---

## Step 2: Choose a Workspace

Don't create projects randomly on your Desktop.

Create a dedicated workspace.

### Windows

```powershell
mkdir D:\Projects
cd D:\Projects
```

#

### Linux

```bash
mkdir -p ~/projects
cd ~/projects
```

Check where you are:

```bash
pwd
```

Example:

```text
/home/baloram/projects
```

---

## Step 3: Create the Project

- Run:

  ```bash
  npx create-next-app@latest my-first-next-app
  ```

- Let's break this command down:

  | Part                | Meaning                                      |
  | ------------------- | -------------------------------------------- |
  | `npx`               | Run a package without installing it globally |
  | `create-next-app`   | Official project generator                   |
  | `@latest`           | Use the latest version                       |
  | `my-first-next-app` | Name of your project folder                  |

- Behind the scenes:

  ```text
  npx
    │
    ▼
  Downloads create-next-app
    │
    ▼
  Creates project folder
    │
    ▼
  Creates files
    │
    ▼
  Installs React
    │
    ▼
  Installs Next.js
    │
    ▼
  Installs dependencies
    │
    ▼
  Project Ready
  ```

---

## Step 4: Answer the Questions

You'll see prompts similar to these.

### 1. TypeScript


Would you like to use `TypeScript`?

Choose:

```text
Yes
```

### Why?

TypeScript helps catch mistakes while coding.

Nearly all modern Next.js projects use it.

---

### 2. ESLint


Would you like to use `ESLint`?

Choose:

```text
Yes
```

ESLint checks your code for mistakes and encourages consistent coding style.

---

### 3. Tailwind CSS

Would you like to use `Tailwind CSS`?

Choose:

```text
Yes
```

Tailwind is a popular CSS framework. It is optional, but it's a good choice for learning modern Next.js development.

---

### 4. src Directory


Would you like your code inside a `src/` directory? Choose:

```text
Yes
```

This keeps your project organized.

- Instead of:

  ```text
  app/
  components/
  ```

- You'll have:

  ```text
  src/
    app/
    components/
  ```

---

### 5. App Router


Would you like to use `App Router`? Choose:

```text
Yes
```

This is the modern routing system introduced in Next.js 13 and is now the standard.

---

### 6. Turbopack

Would you like to use `Turbopack` for `next dev`? Choose:

```text
Yes
```

Turbopack provides a faster development experience.

---

## 7. Import Alias


Would you like to customize the import `alias`? Choose:

```text
No
```

The default alias `@/*` is suitable for most projects.

---

## Final Answers

- Your selections should look like this:

  ```text
  ✔ TypeScript?                     Yes
  ✔ ESLint?                         Yes
  ✔ Tailwind CSS?                   Yes
  ✔ src/ directory?                 Yes
  ✔ App Router?                     Yes
  ✔ Turbopack?                      Yes
  ✔ Customize import alias?         No
  ```

---

## Step 5: Wait for Installation

Next.js will install packages automatically.

- You'll see messages like:

  ```text
  Installing dependencies...

  react
  react-dom
  next

  added 350 packages
  ```

- When it's done:

  ```text
  Success!

  Created my-first-next-app
  ```

---

## Step 6: Enter the Project

- Go to project directory

  ```bash
  cd my-first-next-app
  ```

---

## Step 7: Verify the Project

List the files.

- Windows

  ```powershell
  dir
  ```

- Linux

  ```bash
  ls
  ```

- You should see something similar to:

  ```text
  README.md
  next.config.ts
  package.json
  package-lock.json
  tsconfig.json
  src/
  public/
  node_modules/
  ```

Don't worry about what these files do yet—we'll explore them in the next lesson.

---

## Step 8: Start the Development Server

- Run:

  ```bash
  npm run dev
  ```

- You'll see output similar to:

  ```text
  ▲ Next.js

  Local:    http://localhost:3000
  Network:  http://192.168.x.x:3000

  Ready in 2.0s
  ```

---

## Step 9: Open the Browser

- Visit:

  ```text
  http://localhost:3000
  ```

You should see the default Next.js welcome page.

Congratulations! 🎉 Your first Next.js application is running.

---

## Step 10: Stop the Server

- Return to the terminal and press:

  ```text
  Ctrl + C
  ```

---

## What Just Happened?

- When you ran:

  ```bash
  npm run dev
  ```

  >npm looked inside `package.json` for the `dev` script and executed it.

- The flow looks like this:

  ```text
  You
  │
  ▼
  npm run dev
  │
  ▼
  package.json
  │
  ▼
  next dev
  │
  ▼
  Turbopack starts
  │
  ▼
  Development server starts
  │
  ▼
  http://localhost:3000
  ```

  >We'll inspect `package.json` in detail in a later lesson.

---


