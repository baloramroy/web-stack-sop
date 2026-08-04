**Phase 9 — API Routes**

# Lesson 2: Create Your First GET API

Today you'll create your first API route that returns JSON.


## Step 1 — Understand the Folder Structure

Inside your project, create these folders:

```text
src/
└── app/
    └── api/
        └── hello/
            └── route.ts
```

Notice something important.

For a page, we create:

```text
page.tsx
```

For an API, we create:

```text
route.ts
```

This is the App Router convention.

---

## Step 2 — Create `route.ts`

Create this file:

```text
src/app/api/hello/route.ts
```

Add the following code:

```typescript
export async function GET() {
  return Response.json({
    message: "Hello from Next.js API!"
  });
}
```

Let's understand every line instead of just copying it.

---

## Understanding the Code

### Line 1

```typescript
export async function GET()
```

#

### `export`

Makes this function available to Next.js.

Without it, Next.js cannot use your API route.

#

### `async`

This means the function can perform asynchronous operations.

Right now we're not using any asynchronous code, but later you'll fetch data from:

* Databases
* External APIs
* Files

Those operations take time, so Next.js encourages using `async` from the beginning.

#

### `GET`

This is the HTTP method.

When someone sends a **GET request**, Next.js automatically calls this function.

Think of it like this:

```text
Browser

↓

GET /api/hello

↓

Next.js

↓

Calls GET()
```

You didn't call the function yourself.

Next.js calls it for you.

---

## Line 2

```typescript
return Response.json({
```

We're returning a response.

Not HTML.

Not JSX.

Not a React component.

We're returning **JSON**.

#

`Response.json()` creates a proper HTTP response with:

* Status Code: `200 OK`
* Content-Type: `application/json`
* JSON body

You don't have to set these manually for this simple case.

---

## Line 3

```typescript
message: "Hello from Next.js API!"
```

This is the JSON data.

The response body becomes:

```json
{
  "message": "Hello from Next.js API!"
}
```

---

## Step 3 — Run the Development Server

If it isn't already running:

```bash
npm run dev
```

You should see something similar to:

```text
▲ Next.js

Ready in 2.1s
```

---

## Step 4 — Open Your API

Instead of visiting:

```text
http://localhost:3000/
```

visit:

```text
http://localhost:3000/api/hello
```

---

Instead of a webpage, you'll see:

```json
{
  "message": "Hello from Next.js API!"
}
```

Congratulations!

You've just created your first backend endpoint in Next.js.

---

## What Just Happened?

Let's visualize the flow.

```text
Browser

        │

GET /api/hello

        │

Next.js App Router

        │

route.ts

        │

GET()

        │

Response.json()

        │

JSON Response

        │

Browser
```

This is the complete request lifecycle for today's lesson.

---

## Compare It with a Page

A page:

```text
src/app/about/page.tsx
```

returns:

```tsx
<h1>About Page</h1>
```

An API:

```text
src/app/api/hello/route.ts
```

returns:

```json
{
  "message": "Hello from Next.js API!"
}
```

So remember:

| `page.tsx`              | `route.ts`             |
| ----------------------- | ---------------------- |
| Builds a webpage        | Builds an API endpoint |
| Returns UI (React/HTML) | Returns data (JSON)    |
| Opened as a page        | Called to get data     |

---

## Mini Exercise

Create another API route.

Create this folder:

```text
src/app/api/student/
```

Inside it, create:

```text
route.ts
```

Return this JSON:

```json
{
  "name": "Baloram",
  "course": "Next.js",
  "phase": 9
}
```

Then visit:

```text
http://localhost:3000/api/student
```

You should see the JSON response in your browser.

---

## Common Beginner Mistakes

### ❌ Mistake 1

Creating:

```text
page.tsx
```

inside:

```text
api/
```

For APIs, always create:

```text
route.ts
```

#

### ❌ Mistake 2

Returning JSX:

```tsx
return <h1>Hello</h1>
```

API routes return data, not UI.

#

### ❌ Mistake 3

Forgetting to export the function:

```typescript
function GET() {}
```

It must be:

```typescript
export async function GET() {}
```

---

## Lesson Summary

Today you learned:

* ✅ How to create your first API route.
* ✅ Why API routes use `route.ts`.
* ✅ How the `GET()` function is invoked automatically by Next.js.
* ✅ How to return JSON using `Response.json()`.
* ✅ How to test an API in the browser.
* ✅ The difference between a page (`page.tsx`) and an API (`route.ts`).

---

## Next Lesson

We will **stay in Lesson 2** and go a little deeper before moving to POST.

In the next lesson, you'll learn:

* Returning different JSON structures
* Setting custom HTTP status codes (such as `200` and `404`)
* Returning arrays and nested objects
* Understanding the response object in more detail

We won't move to **Lesson 3 (POST)** until you're comfortable with building and understanding **GET** APIs. This keeps us consistent with the roadmap and builds a solid foundation before introducing additional HTTP methods.
