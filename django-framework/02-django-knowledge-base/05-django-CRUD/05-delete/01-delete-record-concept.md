Exactly. We are starting the **final CRUD operation: Delete**.

We’ll keep the roadmap and our learning style consistent: **first understand the concept, then implement it step by step.** 

# Phase 5 → CRUD → Delete

## Lesson 1: Understanding Delete

So far we have:

```text
CRUD

C → Create        ✅
R → Read          ✅
U → Update        ✅
D → Delete        ← We are here
```

Delete means removing an existing record from the database.

For example, suppose we have:

| ID | Name  | Email                                         |
| -: | ----- | --------------------------------------------- |
|  1 | John  | [john@example.com](mailto:john@example.com)   |
|  2 | Alice | [alice@example.com](mailto:alice@example.com) |
|  3 | Bob   | [bob@example.com](mailto:bob@example.com)     |

If we delete Alice:

```text
ID = 2
```

the database becomes:

| ID | Name | Email                                       |
| -: | ---- | ------------------------------------------- |
|  1 | John | [john@example.com](mailto:john@example.com) |
|  3 | Bob  | [bob@example.com](mailto:bob@example.com)   |

The record with ID `2` is gone.

---

# Why Delete Is Different

Create and Update don't normally destroy existing data.

Delete does.

That's why we need to be more careful.

Imagine a user accidentally clicks:

```text
Delete
```

and the record immediately disappears.

There may be no opportunity to undo it.

For that reason, our CRUD application should have a confirmation step.

---

# The Delete Workflow

We won't simply do:

```text
Click Delete
      ↓
Delete immediately
```

Instead:

```text
Student List
      │
      ▼
Click Delete
      │
      ▼
Delete Confirmation Page
      │
      ▼
"Are you sure?"
      │
      ├── No → Go back
      │
      └── Yes → POST
                    │
                    ▼
               Delete record
                    │
                    ▼
                Redirect
```

This gives the user a chance to stop the operation.

---

# Why Not Delete With a Simple Link?

You might initially think:

```html
<a href="/students/2/delete/">
    Delete
</a>
```

This is not the approach we want for our delete operation.

A link normally represents navigation—a **GET** request.

But deletion changes the database.

We generally don't want a simple GET request to perform destructive actions.

For example, if a browser, crawler, preview system, or user accidentally requests:

```text
/students/2/delete/
```

we don't want that request alone to destroy the record.

Instead, the deletion should happen through a deliberate **POST** submission.

---

# GET vs POST

This is an important concept.

### GET

Used when we want to **retrieve/display** something.

Examples we've already built:

```text
/students/
```

```text
/students/2/
```

```text
/students/2/edit/
```

These pages display information.

---

### POST

Used when the user submits an operation that changes data.

We've already used POST for:

```text
Create
```

and:

```text
Update
```

We'll use POST for:

```text
Delete
```

So our general rule becomes:

```text
GET  → Display
POST → Change data
```

It's a simplified rule, but it's a very useful mental model at this stage.

---

# What Will Our Delete Page Look Like?

Suppose the user wants to delete Alice.

They click:

```text
Delete
```

and Django opens:

```text
/students/2/delete/
```

The page might display:

```text
Delete Student

Are you sure you want to delete:

Name: Alice
Email: alice@example.com
Age: 21


[ Cancel ]    [ Delete ]
```

The important part is that **nothing has been deleted yet**.

The user is only viewing the confirmation page.

---

# The Two Requests

This is important.

When the user first opens:

```text
/students/2/delete/
```

the request is:

```text
GET
```

Django:

```text
GET
 ↓
Find Student 2
 ↓
Show confirmation page
```

Nothing is deleted.

---

Then the user clicks:

```text
Delete
```

The form sends:

```text
POST
```

Django:

```text
POST
 ↓
Find Student 2
 ↓
Delete Student 2
 ↓
Redirect to Student List
```

This separation makes the operation much safer.

---

# How Django Will Find the Student

Just like our Detail and Update views, we'll use:

```python
get_object_or_404()
```

For example:

```python
student = get_object_or_404(
    Student,
    id=id
)
```

Why?

Because the student might not exist.

If someone tries:

```text
/students/999/delete/
```

and student `999` doesn't exist, Django should return:

```text
404 Not Found
```

rather than producing an unexpected error.

You've already learned this pattern, so Delete will reinforce it.

---

# The Delete Operation Itself

Once the user confirms the deletion, Django will eventually execute:

```python
student.delete()
```

This is the key method we'll learn next.

Conceptually:

```text
student
   │
   ▼
student.delete()
   │
   ▼
Database
   │
   ▼
Student record removed
```

Notice the difference:

### Update

```python
student.save()
```

means:

> Save changes to this existing object.

### Delete

```python
student.delete()
```

means:

> Remove this object from the database.

---

# Complete Delete Flow

Putting everything together:

```text
                 Student List
                      │
                      ▼
                Click "Delete"
                      │
                      ▼
             /students/2/delete/
                      │
                      ▼
                    GET
                      │
                      ▼
             get_object_or_404()
                      │
                      ▼
             Confirmation Page
                      │
                      ▼
             User clicks "Delete"
                      │
                      ▼
                    POST
                      │
                      ▼
               student.delete()
                      │
                      ▼
              Database Record
                  Removed
                      │
                      ▼
                 Redirect
                      │
                      ▼
                Student List
```

That's the complete architecture we'll build.

---

# Today's Key Lessons

Today you learned:

* ✅ Delete removes an existing database record.
* ✅ Delete is a destructive operation, so we should confirm it.
* ✅ A simple GET request should not perform the deletion.
* ✅ The confirmation page can be loaded with GET.
* ✅ The actual deletion should happen through POST.
* ✅ `get_object_or_404()` can safely retrieve the object before deletion.
* ✅ `student.delete()` will eventually remove the record.
* ✅ After deletion, we'll redirect the user back to the list.

---

# CRUD Is Almost Complete

Your current Django CRUD knowledge now looks like this:

```text
CREATE
   │
   └── POST → Create record

READ
   │
   ├── GET → List records
   └── GET → Detail record

UPDATE
   │
   └── POST → Update record

DELETE
   │
   ├── GET  → Confirmation page
   └── POST → Delete record
```

That's a very important foundation.

## Next Step

In the next lesson, we'll create the Delete URL and view:

```python
path(
    "students/<int:id>/delete/",
    views.student_delete,
    name="student_delete"
)
```

Then we'll retrieve the student and build the **confirmation page**—still without deleting anything yet.
