**Phase 9 — API Routes**

# Lesson 5 (Practical): Testing POST APIs

So today we're not learning any new HTTP methods. Instead, we're going to learn **how a client actually sends a POST request to our API**.

---

## Goal:

Flow

```text
Client

      │

Send POST Request

      │

Next.js API

      │

Read Request Body

      │

Return Response

      │

Client Receives Response
```

By the end of this lesson, you'll understand the **complete request-response cycle**.

---

# The Problem

With GET, we simply visited:

```text
http://localhost:3000/api/student
```

The browser automatically sent:

```http
GET /api/student
```

Easy.

---

But how do we send:

```http
POST /api/student
```

The browser address bar **cannot do this**.

Typing:

```text
http://localhost:3000/api/student
```

always sends:

```http
GET
```

Never POST.

So we need another way.

---

# Four Common Ways to Test APIs

There are many API testing tools, but these four are the most common:

```text
1. Postman

2. Thunder Client

3. curl

4. fetch()
```

We'll learn them in this order because it matches how you'll work in real projects.

---

# Method 1 — Postman

Imagine you're working as a backend developer.

The frontend isn't finished yet.

How do you test your API?

Use **Postman**.

It lets you manually create HTTP requests.

Example:

```text
POST

↓

URL

↓

Headers

↓

Body

↓

Send
```

Then you immediately see the response.

---

# Example

Choose:

```text
Method

POST
```

URL

```text
http://localhost:3000/api/student
```

Body

```json
{
    "name": "Baloram",
    "course": "Next.js"
}
```

Click:

```text
Send
```

Response:

```json
{
    "message": "Student received successfully!",
    "data": {
        "name": "Baloram",
        "course": "Next.js"
    }
}
```

Very simple.

---

# Method 2 — Thunder Client

Thunder Client is a VS Code extension.

Think of it as:

```text
Postman

↓

Inside VS Code
```

You don't have to switch between applications.

If you're already coding in VS Code, it's very convenient.

The steps are almost identical:

```text
Choose POST

↓

Enter URL

↓

Add JSON Body

↓

Send
```

---

# Method 3 — curl

Now let's learn something every backend developer should know.

`curl` works directly from the terminal.

Example:

```bash
curl -X POST http://localhost:3000/api/student \
-H "Content-Type: application/json" \
-d '{
  "name":"Baloram",
  "course":"Next.js"
}'
```

Let's break it down.

---

### `-X POST`

```bash
-X POST
```

Means:

```text
Use POST method
```

---

### URL

```bash
http://localhost:3000/api/student
```

This is the endpoint we're calling.

---

### Header

```bash
-H "Content-Type: application/json"
```

This tells the server:

```text
"I'm sending JSON."
```

Without this header, the server may not interpret the body correctly.

---

### Data

```bash
-d
```

Means:

```text
Request Body
```

Everything after `-d` becomes the JSON body.

---

# Visualizing curl

```text
curl

      │

Creates HTTP Request

      │

POST

      │

JSON Body

      │

Next.js

      │

POST()

      │

Response

      │

Terminal
```

---

# Method 4 — fetch()

This is the most important one because **your Next.js frontend will use it**.

Suppose you have a button.

When the user clicks it:

```text
Button

↓

fetch()

↓

POST API

↓

Server

↓

Response

↓

UI Updates
```

Example:

```typescript
async function createStudent() {
    const response = await fetch("/api/student", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify({
            name: "Baloram",
            course: "Next.js",
        }),
    });

    const data = await response.json();

    console.log(data);
}
```

Don't worry about memorizing it. Let's understand it.

---

# Understanding `fetch()`

## URL

```typescript
fetch("/api/student")
```

Where should the request go?

Answer:

```text
/api/student
```

---

## Method

```typescript
method: "POST"
```

This tells the browser:

```text
Don't send GET.

Send POST.
```

---

## Headers

```typescript
headers: {
    "Content-Type": "application/json"
}
```

Exactly the same idea as `curl`.

You're telling the server:

```text
I'm sending JSON data.
```

---

## Body

```typescript
body: JSON.stringify({
    name: "Baloram",
    course: "Next.js"
})
```

Remember from the previous lesson:

The server expects **JSON**.

Inside JavaScript, this:

```typescript
{
    name: "Baloram"
}
```

is a JavaScript object.

To send it over HTTP, it must become a JSON string.

That's what:

```typescript
JSON.stringify()
```

does.

---

# Receiving the Response

After the server responds:

```typescript
const data = await response.json();
```

The response body is converted back into a JavaScript object.

Example:

Server sends:

```json
{
    "message":"Student received successfully!"
}
```

JavaScript receives:

```typescript
{
    message: "Student received successfully!"
}
```

Now you can use it inside your application.

---

# Complete Request-Response Flow

```text
User Clicks Button

        │

fetch()

        │

POST /api/student

        │

Headers

        │

JSON Body

        │

Next.js API

        │

POST()

        │

request.json()

        │

Business Logic

        │

Response.json()

        │

HTTP Response

        │

response.json()

        │

JavaScript Object

        │

Update UI
```

This is the complete lifecycle of a POST request in a Next.js application.

---

# Which Tool Should You Use?

| Tool           | When to Use                                |
| -------------- | ------------------------------------------ |
| Browser        | Testing GET endpoints                      |
| Postman        | Backend/API development and manual testing |
| Thunder Client | API testing without leaving VS Code        |
| `curl`         | Terminal, servers, automation, and scripts |
| `fetch()`      | Real frontend applications                 |

As a Next.js developer, you'll likely use **all five** at different times.

---

# Mini Exercise

Using your existing `/api/student` POST endpoint:

### Exercise 1

Use **Postman** or **Thunder Client** to send:

```json
{
    "name": "Alice",
    "course": "React"
}
```

Observe the response.

---

### Exercise 2

Use `curl` to send:

```json
{
    "name": "Bob",
    "course": "Next.js"
}
```

---

### Exercise 3

Create a temporary page with a button that calls `fetch()` and logs the response to the browser console.

Don't worry about making it look nice—our goal is simply to see the request travel from the browser to the API and back.

---

# Lesson Summary

Today you learned:

* ✅ Why the browser address bar cannot send POST requests.
* ✅ Four common ways to test a POST API.
* ✅ How `curl` builds an HTTP request.
* ✅ How `fetch()` sends JSON to your Next.js API.
* ✅ Why `JSON.stringify()` is needed.
* ✅ How `response.json()` converts the response back into a JavaScript object.
* ✅ The complete POST request-response lifecycle.

---

# Next Lesson

With **Lesson 5 (POST)** now complete, our roadmap takes us to:

## **Phase 9 → Lesson 6**

We'll learn two more HTTP methods together:

* **PUT** — Update existing data.
* **DELETE** — Remove existing data.

We'll follow the same approach as before:

1. Theory
2. Visual explanation
3. Hands-on code
4. Practical examples
5. Common mistakes

No database yet—just understanding how these HTTP methods work in Next.js.
