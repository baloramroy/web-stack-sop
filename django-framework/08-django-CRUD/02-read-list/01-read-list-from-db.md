**Phase 5 → CRUD**

# Topic: Read (List) 

## Today's Goal

Until now, we have been **adding** students.

Now we want to **see** all students stored in the database.

Suppose your database contains:

| ID | Name  | Email                                         | Age |
| -- | ----- | --------------------------------------------- | --- |
| 1  | John  | [john@example.com](mailto:john@example.com)   | 22  |
| 2  | Alice | [alice@example.com](mailto:alice@example.com) | 21  |
| 3  | Bob   | [bob@example.com](mailto:bob@example.com)     | 24  |

We want Django to display them in the browser.

---

## What Does "Read (List)" Mean?

"Read" means **retrieve data** from the database.

There are two common types of Read operations:

1. **Read (List)** → Show many records.
2. **Read (Detail)** → Show one specific record.

Today we'll only learn **Read (List)**.

---

## The Request Flow

The flow is very similar to what you've already learned:

```text
Browser
    │
    ▼
/students/
    │
    ▼
urls.py
    │
    ▼
student_list()
    │
    ▼
Student.objects.all()
    │
    ▼
Database
    │
    ▼
Template
    │
    ▼
Browser
```

Notice something important.

During **Create**, data flowed **from the browser to the database**.

```text
Browser
    │
    ▼
Database
```

During **Read**, the direction is the opposite.

```text
Database
    │
    ▼
Browser
```

This is the biggest conceptual difference.

---

## Step 1 — Create a New View

Open:

```text
views.py
```

Add a new view below `student_create()`:

```python
from django.shortcuts import render, redirect
from .models import Student


def student_list(request):

    students = Student.objects.all()

    return render(
        request,
        "myapp/student_list.html",
        {
            "students": students
        }
    )
```

Don't worry about the template yet.

Let's understand this view first.

---

## Understanding `Student.objects.all()`

This is the most important line in today's lesson:

```python
students = Student.objects.all()
```

Let's break it down.

### `Student`

This is your model.

```python
class Student(models.Model):
    ...
```

#

### `objects`

Every Django model automatically has a **Manager** called `objects`.

Think of it as the gateway to the database.

Whenever you want to:

* create data,
* read data,
* update data,
* delete data,

you usually start with:

```python
Student.objects
```

#

### `all()`

The `all()` method means:

> "Give me every Student record in the database."

If your database contains:

| ID | Name  |
| -- | ----- |
| 1  | John  |
| 2  | Alice |
| 3  | Bob   |

then:

```python
students = Student.objects.all()
```

returns all three student records.

You can think of it as:

```text
[
    Student(John),
    Student(Alice),
    Student(Bob)
]
```

In Django, this isn't actually a Python list—it's a **QuerySet**. A QuerySet behaves similarly to a collection of model objects and is designed for querying the database efficiently. We'll explore QuerySets in more detail later. For now, it's enough to think of it as "all the students."

---

## Step 2 — Pass the Data to the Template

This part:

```python
return render(
    request,
    "myapp/student_list.html",
    {
        "students": students
    }
)
```

passes the retrieved students to the template.

The dictionary:

```python
{
    "students": students
}
```

is called the **context**.

Remember Phase 1?

You learned:

```python
context = {
    "name": "Baloram",
    "course": "Django"
}
```

This is exactly the same concept.

The only difference is that now we're passing a QuerySet instead of simple strings.

---

## Step 3 — Add a URL

Open your app's `urls.py`:

```python
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
]
```

Now visiting:

```text
/students/
```

will execute:

```python
student_list()
```

---

## Step 4 — Create the Template

Create:

```text
templates/
    myapp/
        student_list.html
```

For today, keep it very simple:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Students</title>
</head>
<body>

    <h1>Student List</h1>

    {{ students }}

</body>
</html>
```

---

## Step 5 — Test It

Run:

```bash
python manage.py runserver
```

Open:

```text
http://127.0.0.1:8000/students/
```

You won't see a nicely formatted table yet.

Instead, you'll see something similar to:

```text
<QuerySet [
    <Student: Student object (1)>,
    <Student: Student object (2)>,
    <Student: Student object (3)>
]>
```

or, depending on whether you've defined a `__str__()` method in your model, you may see:

```text
<QuerySet [
    <Student: John>,
    <Student: Alice>,
    <Student: Bob>
]>
```

This confirms something very important:

* ✅ Django connected to the database.
* ✅ `Student.objects.all()` executed successfully.
* ✅ The QuerySet reached the template.

We haven't displayed the students nicely yet—that's the next step.

---

## What We Learned Today

Today you learned the first database query in Django:

```python
students = Student.objects.all()
```

and how to pass the result to a template using the context.

The complete flow is now:

```text
Browser
      │
      ▼
/students/
      │
      ▼
student_list()
      │
      ▼
Student.objects.all()
      │
      ▼
Database
      │
      ▼
QuerySet
      │
      ▼
Template
      │
      ▼
Browser
```

Notice that we still haven't used a `for` loop.

That's intentional.

We first needed to understand **how data gets from the database to the template** before learning **how to display each student**.

---

## Next Lesson

We'll take the `students` QuerySet and use Django's template language:

```django
{% for student in students %}
```

to display every student in a clean HTML table. This is where you'll see how Django templates work with QuerySets to build a proper **Read (List)** page.
