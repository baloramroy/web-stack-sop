**Phase 5 → CRUD → Read (Detail)**
# Lesson: Retreive Specific Reconrd From DataBases

Last lesson, Django extracted the student ID from the URL:

```text
/students/2/
```

and passed it to our view as:

```python
id = 2
```

Today we'll use that ID to retrieve **one specific student** from the database.

---

## Today's Goal

When a user visits:

```text
/students/2/
```

Django should:

1. Read the ID from the URL.
2. Find the student whose ID is `2`.
3. Send that student to the template.
4. Display the student's information.

The complete flow becomes:

```text
Browser
     │
     ▼
/students/2/
     │
     ▼
urls.py
     │
     ▼
student_detail(request, id=2)
     │
     ▼
Student.objects.get(id=2)
     │
     ▼
Database
     │
     ▼
One Student Object
     │
     ▼
Template
     │
     ▼
Browser
```

---

## Step 1 — Understanding `get()`

During Read (List), we wrote:

```python
students = Student.objects.all()
```

What did it return?

```
John
Alice
Bob
```

Or, more accurately:

```text
QuerySet
```

containing multiple students.

#

Now suppose the URL is:

```text
/students/2/
```

We don't want every student.

We only want:

```
Alice
```

That's why Django provides:

```python
Student.objects.get()
```

Read it like English:

> "Get one Student object."

---

# `all()` vs `get()`

| Method                  | Returns                      | Used For    |
| ----------------------- | ---------------------------- | ----------- |
| `Student.objects.all()` | Many students (a QuerySet)   | List page   |
| `Student.objects.get()` | One student (a model object) | Detail page |

This is the biggest difference.

---

## Step 2 — Update the View

Open:

```text
views.py
```

Replace your temporary view with:

```python
from django.shortcuts import render, redirect
from .models import Student


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

Let's understand each line carefully.

---

## Line 1

```python
student = Student.objects.get(id=id)
```

The left side:

```python
student
```

is just a Python variable.

---

The right side:

```python
Student.objects.get(...)
```

asks Django to retrieve **one student**.

#

Inside `get()`:

```python
id=id
```

The first `id` is the **model field**.

Your model contains:

```python
class Student(models.Model):

    name = models.CharField(...)
    email = models.EmailField(...)
    age = models.IntegerField(...)
```

Every Django model also has an automatic primary key field named `id` unless you define your own.

So this means:

> Find the row where the model's `id` field matches the value passed into the view.

---

The second `id`:

```python
id
```

is the value extracted from the URL.

Example:

User visits:

```text
/students/2/
```

Django calls:

```python
student_detail(request, id=2)
```

Now the code becomes:

```python
student = Student.objects.get(id=2)
```

Django queries the database and returns the student with ID 2.

---

## Step 3 — Pass the Student to the Template

This part:

```python
{
    "student": student
}
```

creates the context.

Remember Read (List)?

We passed:

```python
{
    "students": students
}
```

Notice the difference:

#

### List

```python
students
```

Plural.

Many students.

#

### Detail

```python
student
```

Singular.

Only one student.

---

## Step 4 — Update the Template

Open:

```text
templates/myapp/student_detail.html
```

Replace it with:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Student Detail</title>
</head>
<body>

<h1>Student Detail</h1>

<p><strong>ID:</strong> {{ student.id }}</p>

<p><strong>Name:</strong> {{ student.name }}</p>

<p><strong>Email:</strong> {{ student.email }}</p>

<p><strong>Age:</strong> {{ student.age }}</p>

</body>
</html>
```

Notice that we **didn't use a `for` loop**.

Why?

Because we're displaying **one student**, not many.

---

## What Happens Internally?

Suppose the database contains:

| ID | Name  | Email                                         | Age |
| -- | ----- | --------------------------------------------- | --- |
| 1  | John  | [john@example.com](mailto:john@example.com)   | 22  |
| 2  | Alice | [alice@example.com](mailto:alice@example.com) | 21  |
| 3  | Bob   | [bob@example.com](mailto:bob@example.com)     | 24  |

The user visits:

```text
/students/2/
```

The flow is:

```text
URL
 │
 ▼
id = 2
 │
 ▼
Student.objects.get(id=2)
 │
 ▼
Database
 │
 ▼
Alice
 │
 ▼
student variable
 │
 ▼
Context

{
    "student": Alice
}
 │
 ▼
Template
 │
 ▼
{{ student.name }}
 │
 ▼
Alice
```

---

## Step 5 — Test It

Run:

```bash
python manage.py runserver
```

Visit:

```text
http://127.0.0.1:8000/students/1/
```

You should see John's information.

Now visit:

```text
http://127.0.0.1:8000/students/2/
```

You should see Alice's information.

Now try:

```text
http://127.0.0.1:8000/students/3/
```

You should see Bob's information.

The same page displays different data because the ID in the URL changes.

---

## What We Learned Today

Today you learned:

* ✅ How `Student.objects.get()` retrieves one model object.
* ✅ The difference between `all()` and `get()`.
* ✅ How to pass a single model object to a template.
* ✅ Why a detail page doesn't need a `for` loop.
* ✅ How the URL ID controls which record is displayed.

---

## One Important Question

What happens if someone visits:

```text
/students/999/
```

but there is **no student** with ID 999?

Your current code:

```python
student = Student.objects.get(id=id)
```

will raise an exception, and Django will display an error page.

This isn't a good user experience.

---

## Next Lesson

We'll make the detail page production-ready by replacing:

```python
Student.objects.get(id=id)
```

with Django's safer helper:

```python
get_object_or_404(Student, id=id)
```

You'll learn what a **404 Not Found** response is, why it's better than a server error, and why `get_object_or_404()` is the standard approach for Django detail views.
