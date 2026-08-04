**Phase 9 — API Routes**

# Lesson 4 (Deep Dive): Post API

* ✅ Lesson 1 — Create First API (Completed)
* ✅ Lesson 2 — Create Your First GET API (Completed)
* ✅ Lesson 3 — GET API in Depth (Completed)
* 🚀 **Lesson 4 — POST**

---

## Learn only:

```text
POST
```

Goal:

```text
Client

      │

Send Data

      │

POST Request

      │

Next.js API Route

      │

Read Data

      │

Return JSON Response

      │

Client
```

That's it.

Just understand **how a POST request sends data to your API**.

---

# Before We Write Code

In the previous lesson, the browser **asked for data**.

Example:

```text
GET /api/student
```

The server replied:

```json
{
  "name": "Baloram",
  "course": "Next.js"
}
```

The browser didn't send any information.

It only requested data.

---

A **POST** request is different.

Now the client sends information **to** the server.

Example:

```text
POST /api/student
```

with this data:

```json
{
  "name": "Baloram",
  "course": "Next.js"
}
```

The server receives it, processes it, and sends a response back.

---

# Real-Life Analogy

Imagine a registration desk.

### GET

```text
You

↓

"Can you show me my registration?"

↓

Staff

↓

Returns your information
```

You're only asking for information.

---

### POST

```text
You

↓

"Here is my registration form."

↓

Staff

↓

Reads your form

↓

Confirms registration
```

Now you're **submitting** information.

---

# Where Does POST Live?

Exactly where GET lives.

Project structure:

```text
src/
└── app/
    └── api/
        └── student/
            └── route.ts
```

The same `route.ts` file can handle multiple HTTP methods.

---

# GET and POST Together

A single `route.ts` can contain both:

```typescript
export async function GET() {
    // Return data
}

export async function POST() {
    // Receive data
}
```

Next.js automatically chooses the correct function based on the HTTP method.

```text
GET Request
      │
      ▼
GET()

----------------

POST Request
      │
      ▼
POST()
```

---

# Creating Your First POST API

Create or update:

```text
src/app/api/student/route.ts
```

```typescript
export async function POST(request: Request) {
  const body = await request.json();

  return Response.json({
    message: "Student received successfully!",
    data: body,
  });
}
```

Let's understand every line.

---

# Line 1

```typescript
export async function POST(request: Request)
```

### `POST`

This function is automatically called when a POST request reaches this route.

---

### `request`

Unlike the GET example, POST usually needs to **receive** data.

That data arrives inside the `Request` object.

Think of it as a package delivered to your server.

```text
Client

↓

Request

↓

Server
```

The `request` object contains:

* HTTP method
* Headers
* URL
* Body (the data being sent)

Today we'll focus only on the **body**.

---

# Reading the Body

```typescript
const body = await request.json();
```

This is one of the most important lines in a POST handler.

What happens?

```text
Incoming Request

↓

JSON Data

↓

request.json()

↓

JavaScript Object
```

Suppose the client sends:

```json
{
  "name": "Baloram",
  "course": "Next.js"
}
```

After:

```typescript
const body = await request.json();
```

The variable `body` becomes:

```typescript
{
  name: "Baloram",
  course: "Next.js"
}
```

Now you can work with it like any other JavaScript object.

---

# Why `await`?

Reading the request body is an asynchronous operation.

That's why we write:

```typescript
await request.json();
```

Without `await`, you wouldn't get the parsed object—you'd get a pending Promise instead.

---

# Returning a Response

```typescript
return Response.json({
    message: "Student received successfully!",
    data: body
});
```

If the client sent:

```json
{
  "name": "Baloram",
  "course": "Next.js"
}
```

The response becomes:

```json
{
  "message": "Student received successfully!",
  "data": {
    "name": "Baloram",
    "course": "Next.js"
  }
}
```

Notice how the server is simply echoing back what it received.

---

# Visual Flow

```text
Client

      │

POST /api/student

      │

JSON Body

      │

Next.js

      │

POST(request)

      │

await request.json()

      │

JavaScript Object

      │

Response.json()

      │

JSON Response

      │

Client
```

---

# How Do We Test a POST API?

Unlike GET, simply opening a URL in your browser sends a GET request.

To test a POST endpoint, you need a tool that can send POST requests, such as:

* Postman
* Insomnia
* Thunder Client (VS Code extension)
* `curl`
* Your own frontend application using `fetch()`

We'll use one of these in the next lesson when we practice making POST requests.

---

# GET vs POST

| GET                     | POST                            |
| ----------------------- | ------------------------------- |
| Retrieves data          | Sends data                      |
| Usually no request body | Usually includes a request body |
| `GET()` handler         | `POST()` handler                |
| Read-only operations    | Create or submit operations     |

---

# Mini Exercise

Create a new API route:

```text
src/app/api/company/route.ts
```

Add a `POST()` handler.

Read the incoming JSON:

```json
{
  "company": "Nagad Ltd.",
  "department": "IT Infrastructure"
}
```

Return:

```json
{
  "message": "Company data received!",
  "data": {
    "company": "Nagad Ltd.",
    "department": "IT Infrastructure"
  }
}
```

---

# Common Beginner Mistakes

### ❌ Forgetting `await`

```typescript
const body = request.json();
```

This gives you a Promise, not the parsed data.

Correct:

```typescript
const body = await request.json();
```

---

### ❌ Trying to read the body twice

The request body can only be consumed once. If you call `request.json()` a second time, it will fail because the stream has already been read.

---

### ❌ Using `GET()` for creating data

Creating new resources should use `POST()`, not `GET()`.

---

# Lesson Summary

Today you learned:

* ✅ What a POST request is.
* ✅ The difference between GET and POST.
* ✅ How Next.js automatically calls `POST()`.
* ✅ What the `Request` object contains.
* ✅ How `await request.json()` converts JSON into a JavaScript object.
* ✅ How to send a JSON response using `Response.json()`.

---

# Next Lesson

Before we move to **Lesson 5 (PUT & DELETE)**, I recommend one more practical lesson within Step 33:

* How to test POST APIs using **Postman**, **Thunder Client**, **`curl`**, and **`fetch()`** from a Next.js frontend.
* How to inspect request headers and request bodies.
* How to understand the complete request/response cycle.

Once you're comfortable sending POST requests and receiving responses, we'll move on to **Lesson 4: PUT & DELETE**, keeping our roadmap consistent.
