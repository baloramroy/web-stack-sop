**Phase 9 — API Routes**

# Lesson 3 (Deep Dive): Understanding GET APIs in Depth

---

# What Actually Happens?

When you type:

```text
http://localhost:3000/api/hello
```

you are **not opening a file**.

You are sending an **HTTP Request** to your Next.js server.

Think of it like this:

```text
You

      │

Request

      │

Next.js Server

      │

Find matching API route

      │

Run GET()

      │

Create Response

      │

Send Response

      │

You
```

Notice something important.

You never call:

```ts
GET()
```

Yourself.

Next.js does it automatically.

---

# Who Calls GET()?

Suppose your code is:

```typescript
export async function GET() {
    return Response.json({
        message: "Hello"
    });
}
```

Did you write:

```typescript
GET();
```

No.

So who called it?

Answer:

```text
Next.js Framework
```

Next.js watches every incoming request.

When it sees:

```text
GET /api/hello
```

it says:

> "I found a route.ts file."

Then:

> "This request is GET."

Then:

> "I'll execute the GET() function."

This happens automatically.

---

# Why Is the Function Named GET?

Imagine you wrote:

```typescript
export async function ABC() {

}
```

Will it work?

No.

Why?

Because Next.js looks for specific function names.

These are called **HTTP Method Handlers**.

```text
GET()

POST()

PUT()

PATCH()

DELETE()
```

When a request arrives, Next.js matches the HTTP method with the function name.

Example:

```
GET request
↓

Run GET()

-----------------------

POST request
↓

Run POST()
```

The function name is not your choice—it is part of Next.js's convention.

---

# Understanding `Response`

Let's look again:

```typescript
return Response.json({
    message: "Hello"
});
```

Many beginners think:

> Response is a Next.js object.

It isn't.

`Response` is part of the **Web API (Fetch API)** that Next.js supports on both the server and the browser.

Think of it as a box.

```text
Request

↓

Server

↓

Create Response

↓

Send Response
```

A Response contains more than just data.

---

A Response has:

```text
Status Code

Headers

Body
```

Like this:

```text
HTTP/1.1 200 OK

Content-Type: application/json

{
    "message":"Hello"
}
```

Your browser usually hides these details.

---

# What Does `Response.json()` Actually Do?

This:

```typescript
Response.json({
    message: "Hello"
});
```

is a shortcut.

Internally it's similar to:

```typescript
new Response(
    JSON.stringify({
        message: "Hello"
    }),
    {
        headers: {
            "Content-Type": "application/json"
        }
    }
);
```

Next.js (through the Web API) converts your JavaScript object into JSON and sets the correct headers automatically.

---

# Returning Different JSON

JSON is simply data.

Example 1

```typescript
return Response.json({
    name: "Baloram"
});
```

Result

```json
{
    "name": "Baloram"
}
```

---

Example 2

```typescript
return Response.json({
    name: "Baloram",
    age: 30,
    active: true
});
```

Result

```json
{
    "name": "Baloram",
    "age": 30,
    "active": true
}
```

Notice JSON supports different data types:

* String
* Number
* Boolean
* Object
* Array
* null

---

# Returning Arrays

You are not limited to objects.

Example:

```typescript
return Response.json([
    "Apple",
    "Banana",
    "Orange"
]);
```

Result:

```json
[
    "Apple",
    "Banana",
    "Orange"
]
```

---

# Returning Nested Objects

You can return complex structures.

```typescript
return Response.json({
    student: {
        id: 1,
        name: "Baloram"
    },
    course: {
        title: "Next.js"
    }
});
```

Result:

```json
{
    "student": {
        "id": 1,
        "name": "Baloram"
    },
    "course": {
        "title": "Next.js"
    }
}
```

This is how real APIs usually look.

---

# Returning Multiple Records

Example:

```typescript
return Response.json({
    students: [
        {
            id: 1,
            name: "Alice"
        },
        {
            id: 2,
            name: "Bob"
        }
    ]
});
```

This is much closer to what you'll receive from a database later.

---

# HTTP Status Codes

Every HTTP response includes a status code.

Some common ones are:

| Status | Meaning               |
| ------ | --------------------- |
| 200    | Success               |
| 201    | Created               |
| 400    | Bad Request           |
| 401    | Unauthorized          |
| 403    | Forbidden             |
| 404    | Not Found             |
| 500    | Internal Server Error |

By default:

```typescript
Response.json(...)
```

returns:

```text
200 OK
```

---

# Setting Your Own Status Code

You can customize the response:

```typescript
return Response.json(
    {
        error: "Student not found"
    },
    {
        status: 404
    }
);
```

The response becomes:

```text
Status

404 Not Found
```

Body:

```json
{
    "error": "Student not found"
}
```

This is how APIs communicate both **data** and **the outcome of the request**.

---

# Real-Life Example

Imagine you're building your future **Master Register** application.

Request:

```text
GET /api/users/25
```

If user **25 exists**:

```json
{
    "id": 25,
    "name": "Baloram",
    "department": "IT"
}
```

Status:

```text
200 OK
```

---

If user **25 doesn't exist**:

```json
{
    "error": "User not found"
}
```

Status:

```text
404 Not Found
```

The frontend can use both the JSON body and the status code to decide what to display.

---

# Mini Exercise

Create these API routes:

### 1. `/api/company`

Return:

```json
{
    "company": "Nagad Ltd.",
    "department": "IT Infrastructure"
}
```

---

### 2. `/api/servers`

Return:

```json
[
    {
        "id": 1,
        "hostname": "server01"
    },
    {
        "id": 2,
        "hostname": "server02"
    }
]
```

---

### 3. `/api/error`

Return:

* Status: `404`
* Body:

```json
{
    "error": "Resource not found"
}
```

Visit each endpoint in your browser and observe the responses. If you're curious, you can also inspect the **Network** tab in your browser's Developer Tools to see the status code and headers that accompany the JSON.

---

# Lesson Summary

Today you learned:

* ✅ How Next.js automatically calls `GET()`.
* ✅ Why the function **must** be named `GET`.
* ✅ What the `Response` object represents.
* ✅ Why `Response.json()` is convenient.
* ✅ How to return objects, arrays, and nested JSON.
* ✅ What HTTP status codes are and why they matter.
* ✅ How to return custom status codes like `404`.

---

