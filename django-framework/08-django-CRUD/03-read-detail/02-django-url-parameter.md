**Phase 5 → CRUD → Read (Detail)**

# Lesson: URL Parameters

## Goal

We want URLs like these:

```text
/students/1/

/students/2/

/students/3/
```

Notice something interesting.

The beginning never changes:

```text
/students/
```

Only the last part changes:

```text
1

2

3
```

That changing part is called a **URL parameter**.

---

## Why Do We Need URL Parameters?

Suppose you have 1,000 students.

Should you create 1,000 URLs like this?

```text
/students/john/

/students/alice/

/students/bob/
```

No.

Instead, Django uses **one URL pattern**:

```text
/students/<id>/
```

Then the actual value changes depending on which student the user requests.

Examples:

```text
/students/1/

/students/2/

/students/3/

/students/150/

/students/999/
```

One URL pattern can serve every student.

---

## Step 1 — Update `urls.py`

Open your app's `urls.py`.

Add a new path:

```python
from django.urls import path
from . import views

urlpatterns = [

    path(
        "students/",
        views.student_list,
        name="student_list"
    ),

    path(
        "students/add/",
        views.student_create,
        name="student_create"
    ),

    path(
        "students/<int:id>/",
        views.student_detail,
        name="student_detail"
    ),
]
```

Let's understand the new part carefully.

---

## Understanding `<int:id>`

This part:

```python
<int:id>
```

has **two pieces**.

### Part 1

```python
int
```

This tells Django:

> "The value must be an integer."

Examples that match:

```text
/students/1/

/students/50/

/students/999/
```

Examples that do **not** match:

```text
/students/john/

/students/alice/

/students/abc/
```

Those URLs won't match this route.

#

### Part 2

```python
id
```

This is simply the **variable name**.

Think of it like this:

```python
<int:id>
```

means:

> "Capture the integer from the URL and store it in a variable called `id`."

---

## What Happens Internally?

Suppose the browser requests:

```text
/students/5/
```

Django sees:

```python
students/<int:id>/
```

It matches the URL.

Then it extracts:

```text
5
```

and stores it as:

```python
id = 5
```

Then Django calls your view.

---

## Step 2 — Update the View

Open `views.py`.

Add a new view:

```python
from django.shortcuts import render, redirect
from .models import Student


def student_detail(request, id):

    print(id)

    return render(
        request,
        "myapp/student_detail.html"
    )
```

Notice something new.

Our previous views looked like this:

```python
def student_list(request):
```

Only one parameter:

```python
request
```

Now we have:

```python
def student_detail(request, id):
```

There are **two parameters**.

---

## Where Did `id` Come From?

It was supplied automatically by Django.

Remember this URL:

```python
path(
    "students/<int:id>/",
    views.student_detail,
    name="student_detail"
)
```

When the user visits:

```text
/students/25/
```

Django executes:

```python
student_detail(
    request,
    id=25
)
```

You never call this function yourself.

Django calls it for you.

---

## Step 3 — Test It

Run the server:

```bash
python manage.py runserver
```

Visit:

```text
http://127.0.0.1:8000/students/1/
```

Look at the terminal.

You should see:

```text
1
```

Now visit:

```text
/students/2/
```

Terminal:

```text
2
```

Visit:

```text
/students/15/
```

Terminal:

```text
15
```

Nothing has been retrieved from the database yet.

We're only proving that Django correctly extracts the number from the URL and passes it to the view.

---

## Step 4 — Create a Temporary Template

Create:

```text
templates/
    myapp/
        student_detail.html
```

Add:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Student Detail</title>
</head>
<body>

<h1>Student Detail Page</h1>

<p>Check your terminal to see the ID received from the URL.</p>

</body>
</html>
```

This page is only temporary.

In the next lesson, we'll display the actual student's information here.

---

## Visual Flow

Suppose the browser requests:

```text
/students/7/
```

The flow is:

```text
Browser
      │
      ▼
/students/7/
      │
      ▼
urls.py
      │
Matches:
students/<int:id>/
      │
Extracts:
id = 7
      │
      ▼
student_detail(request, id=7)
      │
print(id)
      │
      ▼
Terminal
```

---

## What We Learned Today

Today you learned one of Django's most important routing features:

* ✅ Dynamic URL patterns using `<int:id>`.
* ✅ How Django extracts values from the URL.
* ✅ How those values become parameters in your view.
* ✅ Why one URL pattern can handle every student instead of creating separate routes.

This mechanism isn't limited to students. You'll use URL parameters for products, orders, employees, servers, tickets, blog posts, and almost every resource in a Django application.

---

## Next Lesson

Now that Django can extract the student ID from the URL, we'll use it to retrieve a single student from the database:

```python
student = Student.objects.get(id=id)
```

You'll learn how `get()` differs from `all()`, how it returns exactly one object, and how to pass that object to the template to build your first complete **Read (Detail)** page.
