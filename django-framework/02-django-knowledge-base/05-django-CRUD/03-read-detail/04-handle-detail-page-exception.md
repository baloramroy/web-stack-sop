**Phase 5 → CRUD → Read (Detail)**

# Lesson: Details Page Exception Handling

Last lesson, our view looked like this:

```python
def student_detail(request, id):

    student = Student.objects.get(id=id)

    return render(
        request,
        "myapp/student_detail.html",
        {
            "student": student
        }
    )
```

This works **only if the student exists**.

Today we'll learn what happens when it doesn't.

---

## Today's Goal

Suppose your database contains:

| ID | Name  |
| -- | ----- |
| 1  | John  |
| 2  | Alice |
| 3  | Bob   |

Everything works for:

```text
/students/1/

/students/2/

/students/3/
```

But what if someone manually types:

```text
/students/999/
```

There is no student with ID **999**.

How should our application respond?

---

## What Happens Right Now?

Our code says:

```python
student = Student.objects.get(id=id)
```

If Django cannot find the student, it raises an exception.

You'll see an error page similar to:

```text
Student matching query does not exist.

DoesNotExist at /students/999/
```

This is called an **exception**.

An exception means:

> "Something happened that the program wasn't prepared to handle."

---

## Why Is This Bad?

Imagine you're building your **Master Register** application.

A user accidentally opens:

```text
/access-request/5000/
```

but request **5000** doesn't exist.

Should the user see a long technical error page?

No.

A normal user shouldn't see internal application errors.

Instead, the application should simply say:

```text
404 Not Found

The requested record does not exist.
```

This is much cleaner and more user-friendly.

---

## What is a 404?

A **404 Not Found** response means:

> "The server is working, but the requested resource doesn't exist."

Examples:

```text
/students/999/

/students/500/

/students/10000/
```

If those IDs don't exist, Django should return:

```text
404 Not Found
```

Notice the difference:

| Situation            | Result                    |
| -------------------- | ------------------------- |
| Programming mistake  | 500 Internal Server Error |
| Record doesn't exist | 404 Not Found             |

A missing student is **not** a programming error.

It's simply a missing resource.

---

## Django's Solution

Instead of writing:

```python
Student.objects.get(id=id)
```

Django provides:

```python
get_object_or_404()
```

Read it like English:

> "Get the object, or if it doesn't exist, automatically return a 404 page."

---

## Step 1 — Import `get_object_or_404`

Open:

```text
views.py
```

Update the import:

```python
from django.shortcuts import (
    render,
    redirect,
    get_object_or_404
)
```

Or, if you prefer a single line:

```python
from django.shortcuts import render, redirect, get_object_or_404
```

Both styles are valid.

---

## Step 2 — Update the View

Replace:

```python
student = Student.objects.get(id=id)
```

with:

```python
student = get_object_or_404(
    Student,
    id=id
)
```

Your complete view becomes:

```python
from django.shortcuts import render, redirect, get_object_or_404
from .models import Student


def student_detail(request, id):

    student = get_object_or_404(
        Student,
        id=id
    )

    return render(
        request,
        "myapp/student_detail.html",
        {
            "student": student
        }
    )
```

---

## Understanding `get_object_or_404()`

Let's break it down.

### First Argument

```python
Student
```

This tells Django:

> "Search in the `Student` model."

#

### Second Argument

```python
id=id
```

This means:

> "Find the student whose `id` field matches the value from the URL."

If the URL is:

```text
/students/2/
```

Django effectively runs:

```python
get_object_or_404(
    Student,
    id=2
)
```

---

## What Happens Internally?

### Case 1 — Student Exists

Database:

| ID | Name  |
| -- | ----- |
| 1  | John  |
| 2  | Alice |
| 3  | Bob   |

User visits:

```text
/students/2/
```

Flow:

```text
URL
 │
 ▼
id = 2
 │
 ▼
get_object_or_404(Student, id=2)
 │
 ▼
Student Found
 │
 ▼
Return Student Object
 │
 ▼
Template
```

Everything works normally.

#

### Case 2 — Student Doesn't Exist

User visits:

```text
/students/999/
```

Flow:

```text
URL
 │
 ▼
id = 999
 │
 ▼
get_object_or_404(Student, id=999)
 │
 ▼
Student Not Found
 │
 ▼
Return 404 Response
 │
 ▼
Browser
```

Instead of crashing with an exception, Django sends a proper **404 Not Found** response.

---

## Why Is This Better?

Using:

```python
Student.objects.get()
```

means **you** are responsible for handling the case where the object doesn't exist.

Using:

```python
get_object_or_404()
```

lets Django handle that situation automatically.

This makes your code:

* Shorter
* Easier to read
* More reliable
* More consistent with Django best practices

That's why you'll see `get_object_or_404()` in many real Django projects.

---

## Test It

Run your server:

```bash
python manage.py runserver
```

Now test these URLs:

```text
/students/1/
```

Expected:

```text
John's details
```

#

```text
/students/2/
```

Expected:

```text
Alice's details
```

---

```text
/students/999/
```

Expected:

A **404 Not Found** page instead of a server error.

---

## What We Learned Today

Today you learned:

* ✅ Why `Student.objects.get()` can raise an exception.
* ✅ What a **404 Not Found** response means.
* ✅ How `get_object_or_404()` works.
* ✅ Why it's the recommended approach for Django detail views.
* ✅ How it improves the user experience without adding complex error-handling code.

---

## Create vs Read (Detail)

Let's compare what you've learned so far:

| Operation     | Main Method                         | Returns                       |
| ------------- | ----------------------------------- | ----------------------------- |
| Create        | `Student.objects.create()`          | Creates a new student         |
| Read (List)   | `Student.objects.all()`             | All students (QuerySet)       |
| Read (Detail) | `get_object_or_404(Student, id=id)` | One student or a 404 response |

Each method has a different purpose, and together they form the foundation of Django CRUD.

---

## Next Lesson

We have now completed the core **Read (Detail)** functionality.

Before moving to **Update**, we'll make the application easier to navigate by adding a **"View Details"** link next to each student in the list page. You'll learn Django's `{% url %}` template tag, how to generate URLs by their **name** instead of hardcoding them, and how to pass the student's ID to create links like:

```text
/students/1/

/students/2/

/students/3/
```

This is the standard way Django templates link one page to another.
