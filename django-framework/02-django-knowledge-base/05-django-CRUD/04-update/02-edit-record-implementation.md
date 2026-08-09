**Phase 5 → CRUD → Update**

# Update Specific Records

Last lesson was conceptual. Today we'll build the **Edit page**. **We are not saving changes yet.** Our goal is simply to display a form that is already filled with the student's existing information.

---

## Today's Goal

When the user visits:

```text
/students/2/edit/
```

they should see:

```text
Edit Student

Name:
[Alice____________]

Email:
[alice@example.com]

Age:
[21______________]

        [ Update ]
```

Notice that the fields already contain the current values from the database.

---

## The Request Flow

Today's flow is:

```text
Browser
     │
     ▼
/students/2/edit/
     │
     ▼
urls.py
     │
     ▼
student_update()
     │
     ▼
get_object_or_404()
     │
     ▼
Database
     │
     ▼
Student Object
     │
     ▼
Template
     │
     ▼
Pre-filled Form
```

Notice that this is almost identical to the **Detail** page.

The only difference is that instead of displaying plain text, we'll display **HTML input fields**.

---

## Step 1 — Add the URL

Open your app's `urls.py`.

Add a new route:

```python
path(
    "students/<int:id>/edit/",
    views.student_update,
    name="student_update"
)
```

Your `urlpatterns` now contains something like:

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

    path(
        "students/<int:id>/",
        views.student_detail,
        name="student_detail"
    ),

    path(
        "students/<int:id>/edit/",
        views.student_update,
        name="student_update"
    ),
]
```

---

## Understanding the URL

Look carefully:

```text
/students/2/
```

means:

> Show Student 2.

But:

```text
/students/2/edit/
```

means:

> Edit Student 2.

The extra:

```text
/edit/
```

tells Django which operation we're performing.

---

## Step 2 — Create the View

Open:

```text
views.py
```

Add:

```python
from django.shortcuts import (
    render,
    redirect,
    get_object_or_404,
)

from .models import Student


def student_update(request, id):

    student = get_object_or_404(
        Student,
        id=id
    )

    return render(
        request,
        "myapp/student_update.html",
        {
            "student": student
        }
    )
```

---

## Understanding the View

This line should already look familiar:

```python
student = get_object_or_404(
    Student,
    id=id
)
```

Where have we seen this before?

In our **Detail** page.

Nothing new is happening here.

If the URL is:

```text
/students/2/edit/
```

Django executes:

```python
student = get_object_or_404(
    Student,
    id=2
)
```

and retrieves Alice from the database.

---

Next:

```python
{
    "student": student
}
```

passes the student object to the template.

Again, exactly like the Detail page.

The difference will be inside the HTML template.

---

## Step 3 — Create the Template

Create:

```text
templates/
    myapp/
        student_update.html
```

Add:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Edit Student</title>
</head>
<body>

<h1>Edit Student</h1>

<form>

    <p>
        <label>Name</label><br>
        <input
            type="text"
            name="name"
            value="{{ student.name }}"
        >
    </p>

    <p>
        <label>Email</label><br>
        <input
            type="email"
            name="email"
            value="{{ student.email }}"
        >
    </p>

    <p>
        <label>Age</label><br>
        <input
            type="number"
            name="age"
            value="{{ student.age }}"
        >
    </p>

    <button type="submit">
        Update
    </button>

</form>

</body>
</html>
```

---

## The Most Important Concept Today

Look at this:

```html
value="{{ student.name }}"
```

During **Create**, we had:

```html
<input type="text" name="name">
```

The input was empty.

Now we have:

```html
<input
    type="text"
    name="name"
    value="{{ student.name }}"
>
```

The `value` attribute tells the browser what should appear inside the input when the page loads.

---

## What Happens Internally?

Suppose the database contains:

| ID | Name  | Email                                         | Age |
| -- | ----- | --------------------------------------------- | --- |
| 2  | Alice | [alice@example.com](mailto:alice@example.com) | 21  |

The view sends:

```python
{
    "student": student
}
```

Inside the template:

```django
{{ student.name }}
```

becomes:

```text
Alice
```

So Django generates:

```html
<input
    type="text"
    name="name"
    value="Alice"
>
```

The browser displays:

```text
Name

[Alice____________]
```

The same happens for:

```django
{{ student.email }}
```

and

```django
{{ student.age }}
```

Every field is automatically pre-filled with the existing data.

---

## Step 4 — Test It

Run:

```bash
python manage.py runserver
```

Visit:

```text
http://127.0.0.1:8000/students/1/edit/
```

You should see John's information already filled in.

Now try:

```text
http://127.0.0.1:8000/students/2/edit/
```

You should see Alice's information.

Then:

```text
http://127.0.0.1:8000/students/3/edit/
```

You should see Bob's information.

The same page works for every student because the ID in the URL determines which record is loaded.

---

## What We Learned Today

Today you learned:

* ✅ How to create an Edit URL using `<int:id>`.
* ✅ How to reuse `get_object_or_404()` to retrieve the student.
* ✅ How to pass a single model object to a template.
* ✅ How the HTML `value` attribute pre-fills form fields.
* ✅ Why the Update form starts with existing data instead of blank fields.

Notice what we **didn't** do today:

* ❌ We didn't use `method="POST"`.
* ❌ We didn't update the database.
* ❌ We didn't call `student.save()`.

That's intentional. We first built the **first half** of the Update operation.

---

## Next Lesson

Now that the form displays the existing data, we'll complete the Update operation. We'll:

1. Change the form to use `method="POST"` and add `{% csrf_token %}`.
2. Read the edited values from `request.POST`.
3. Assign the new values to the existing `student` object.
4. Call:

```python
student.save()
```

This will update the existing database record instead of creating a new one, completing your first full **Update** operation.
