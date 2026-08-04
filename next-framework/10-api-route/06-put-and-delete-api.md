**Phase 9 — API Routes**

# Lesson 6: PUT & DELETE

## Objective

Learn only:

```text
PUT

DELETE
```

Goal:

```text
Client

      │

Update/Delete Request

      │

Next.js API

      │

Modify Resource

      │

Return Response

      │

Client
```

---

# Before We Start

So far you've learned two HTTP methods.

## GET

Meaning:

> "Give me some data."

Example:

```http
GET /api/student
```

---

## POST

Meaning:

> "Here is some new data."

Example:

```http
POST /api/student
```

---

Now imagine you already have a student.

```json
{
    "id": 1,
    "name": "Baloram",
    "course": "Next.js"
}
```

What if the course changes?

Should we use POST again?

No.

Because we're **not creating** a new student.

We're **updating** an existing one.

That's where **PUT** comes in.

---

# What is PUT?

PUT means:

> **Update an existing resource.**

Example:

```http
PUT /api/student/1
```

Body:

```json
{
    "name": "Baloram",
    "course": "React"
}
```

The server updates student **1**.

Notice:

We're changing existing data.

We're not creating new data.

---

# Real-Life Example

Imagine an employee record.

Current record:

```text
Name: Baloram
Department: IT
Phone: 01711111111
```

The employee gets a new phone number.

You don't create a new employee.

You update the existing employee.

That is exactly what PUT is for.

---

# What is DELETE?

DELETE means:

> **Remove an existing resource.**

Example:

```http
DELETE /api/student/1
```

The server removes student **1**.

No new data is sent.

Instead, you're telling the server:

> "Delete this resource."

---

# HTTP Methods So Far

| Method | Purpose              |
| ------ | -------------------- |
| GET    | Read data            |
| POST   | Create new data      |
| PUT    | Update existing data |
| DELETE | Remove existing data |

This is the foundation of REST APIs.

---

# How Does Next.js Know Which Function to Run?

Exactly the same way as GET and POST.

Suppose your `route.ts` contains:

```typescript
export async function GET() {}

export async function POST() {}

export async function PUT() {}

export async function DELETE() {}
```

When a request arrives:

```text
GET Request
      │
      ▼
GET()

--------------------

POST Request
      │
      ▼
POST()

--------------------

PUT Request
      │
      ▼
PUT()

--------------------

DELETE Request
      │
      ▼
DELETE()
```

Again,

**You never call these functions yourself.**

Next.js calls the correct one automatically.

---

# Creating a PUT Handler

Suppose we have:

```text
src/app/api/student/route.ts
```

Add:

```typescript
export async function PUT(request: Request) {
    const body = await request.json();

    return Response.json({
        message: "Student updated successfully!",
        updatedData: body,
    });
}
```

Notice something interesting.

This looks almost identical to POST.

The difference isn't in the code.

The difference is in the **meaning**.

POST:

```text
Create something new.
```

PUT:

```text
Update something that already exists.
```

---

# Visual Flow for PUT

```text
Client

      │

PUT /api/student

      │

JSON Body

      │

Next.js

      │

PUT()

      │

Read Body

      │

Update Resource

      │

Return Response

      │

Client
```

---

# Creating a DELETE Handler

Now add:

```typescript
export async function DELETE() {
    return Response.json({
        message: "Student deleted successfully!"
    });
}
```

For today's lesson, we're keeping it simple.

Later, when we connect MySQL, this function will actually remove data from the database.

Today we're only learning the request flow.

---

# Visual Flow for DELETE

```text
Client

      │

DELETE /api/student

      │

Next.js

      │

DELETE()

      │

Delete Resource

      │

Return Response

      │

Client
```

---

# Typical Responses

### PUT Response

```json
{
    "message": "Student updated successfully!",
    "updatedData": {
        "name": "Baloram",
        "course": "React"
    }
}
```

---

### DELETE Response

```json
{
    "message": "Student deleted successfully!"
}
```

---

# Understanding the Meaning

Imagine your future **Master Register** application.

### Create a user

```http
POST /api/users
```

Creates a new user.

---

### View users

```http
GET /api/users
```

Returns all users.

---

### Update a user's department

```http
PUT /api/users/25
```

Updates user **25**.

---

### Delete a user

```http
DELETE /api/users/25
```

Removes user **25**.

Notice how each HTTP method has a clear responsibility.

---

# Common Beginner Mistakes

### ❌ Using POST for everything

Many beginners write every endpoint as POST.

That works technically, but it loses the meaning of the API.

Use the HTTP method that matches the action.

---

### ❌ Thinking PUT creates new data

PUT is for updating existing resources in our roadmap and examples.

---

### ❌ Returning HTML

Just like GET and POST API routes, PUT and DELETE should return data (typically JSON), not JSX or HTML.

---

# Mini Exercise

Create a new route:

```text
src/app/api/server/route.ts
```

Implement four handlers:

```typescript
GET()

POST()

PUT()

DELETE()
```

Return a different JSON message from each one.

For example:

```json
{
    "message": "Server information retrieved."
}
```

```json
{
    "message": "Server created."
}
```

```json
{
    "message": "Server updated."
}
```

```json
{
    "message": "Server deleted."
}
```

Don't connect a database yet. The goal is simply to understand that **one `route.ts` file can respond to different HTTP methods**.

---

# Lesson Summary

Today you learned:

* ✅ What **PUT** means.
* ✅ What **DELETE** means.
* ✅ The difference between **POST** and **PUT**.
* ✅ How Next.js automatically routes requests to `PUT()` and `DELETE()`.
* ✅ How to return JSON responses from these handlers.
* ✅ How these methods fit into a RESTful API design.

---

# Phase 9 Complete 🎉

You have now completed all the planned API Route lessons in our roadmap:

* ✅ GET
* ✅ POST
* ✅ PUT & DELETE 

You now understand the complete request lifecycle and the four core HTTP methods that you'll use throughout your Next.js applications.

---

# Next Phase

According to our roadmap, the next phase is:

## **Phase 10 — Database**

We'll begin with **Step 35: Learn What an ORM Is**.

Before writing any database code, we'll first understand:

* What a database is.
* Why applications don't usually talk directly to the database.
* What an ORM is.
* Why Next.js commonly uses **Prisma**.
* How data flows between your API routes and the database.

We'll follow the same slow, step-by-step approach we've used throughout the course.
