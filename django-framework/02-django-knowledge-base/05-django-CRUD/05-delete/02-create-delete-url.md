Good. We’ll now implement the **first half of Delete** exactly as planned: URL → view → confirmation page. **We will not delete anything yet.**

The roadmap establishes the CRUD order as **Create → Read (List) → Read (Details) → Update → Delete**, so this is the final CRUD section. 

# Phase 5 → CRUD → Delete

## Step 1 — Create the Delete URL

Open your app's:

```text
myapp/urls.py
```

Add:

```python
path(
    "students/<int:id>/delete/",
    views.student_delete,
    name="student_delete"
)
```

So your relevant URLs now look like:

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

    path(
        "students/<int:id>/delete/",
        views.student_delete,
        name="student_delete"
    ),
]
```

The important new part is:

```python
<int:id>
```

This means Django will capture the student's ID from the URL.

For example:

```text
/students/2/delete/
```

becomes:

```python
id = 2
```

---

# Step 2 — Create the View

Open:

```text
myapp/views.py
```

Add:

```python
def student_delete(request, id):

    student = get_object_or_404(
        Student,
        id=id
    )

    return render(
        request,
        "myapp/student_delete.html",
        {
            "student": student
        }
    )
```

Notice something important.

We are using:

```python
get_object_or_404()
```

just like we did for **Detail** and **Update**.

So if the user visits:

```text
/students/999/delete/
```

and student `999` doesn't exist, Django returns a **404**.

---

# Step 3 — What Does This View Do?

Right now, it does **not delete anything**.

Let's follow the request.

User visits:

```text
/students/2/delete/
```

Django captures:

```python
id = 2
```

Then:

```python
student = get_object_or_404(
    Student,
    id=id
)
```

retrieves student 2.

Then:

```python
return render(...)
```

displays the confirmation page.

So currently:

```text
GET /students/2/delete/
          │
          ▼
Find Student 2
          │
          ▼
Show confirmation page
          │
          ▼
NO DELETION
```

This is intentional.

---

# Step 4 — Create the Confirmation Template

Create:

```text
templates/
└── myapp/
    └── student_delete.html
```

Put this inside:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Delete Student</title>
</head>
<body>

<h1>Delete Student</h1>

<p>
    Are you sure you want to delete this student?
</p>

<p>
    <strong>ID:</strong> {{ student.id }}
</p>

<p>
    <strong>Name:</strong> {{ student.name }}
</p>

<p>
    <strong>Email:</strong> {{ student.email }}
</p>

<p>
    <strong>Age:</strong> {{ student.age }}
</p>

<form method="POST">

    {% csrf_token %}

    <button type="submit">
        Yes, Delete
    </button>

</form>

<a href="{% url 'student_detail' student.id %}">
    Cancel
</a>

</body>
</html>
```

---

# Understand the Confirmation Page

Suppose Alice has:

```text
ID: 2
Name: Alice
Email: alice@example.com
Age: 21
```

When you visit:

```text
/students/2/delete/
```

the page displays:

```text
Delete Student

Are you sure you want to delete this student?

ID: 2
Name: Alice
Email: alice@example.com
Age: 21

[ Yes, Delete ]

Cancel
```

At this point, **Alice is still in the database**.

---

# Why Does the Form Use POST?

Look at:

```html
<form method="POST">
```

We are deliberately separating two things:

### Opening confirmation page

```text
GET
```

means:

> "Show me the confirmation page."

### Clicking Yes, Delete

```text
POST
```

means:

> "I have confirmed the operation."

The actual deletion will happen only when we handle that POST request.

---

# Why `{% csrf_token %}`?

We already used this when creating and updating students:

```django
{% csrf_token %}
```

It protects Django POST forms against **Cross-Site Request Forgery (CSRF)** attacks.

So for our destructive POST operation, it is especially important that we keep it.

---

# Why Is Cancel an `<a>`?

Our Cancel link is:

```django
<a href="{% url 'student_detail' student.id %}">
    Cancel
</a>
```

This generates something like:

```text
/students/2/
```

So clicking **Cancel** simply takes the user back to the student's detail page.

Nothing changes in the database.

---

# Test It

Start Django:

```bash
python manage.py runserver
```

Now visit:

```text
http://127.0.0.1:8000/students/1/delete/
```

You should see the confirmation page.

Try:

```text
/students/2/delete/
```

You should see student 2's information.

Now try a nonexistent student:

```text
/students/999/delete/
```

You should get:

```text
404 Not Found
```

Most importantly, check your database.

**The student should still exist.**

We haven't implemented the deletion yet.

---

# Current Delete Flow

We've now built:

```text
Student
   │
   ▼
/students/2/delete/
   │
   ▼
urls.py
   │
   ▼
student_delete(request, id=2)
   │
   ▼
get_object_or_404()
   │
   ▼
Student Object
   │
   ▼
Confirmation Template
   │
   ▼
[ Yes, Delete ]    [ Cancel ]
```

The next piece is still missing:

```text
[ Yes, Delete ]
        │
        ▼
      POST
        │
        ▼
student.delete()
        │
        ▼
Database
```

---

## What You Learned

Today you implemented:

* ✅ Delete URL with `<int:id>`
* ✅ Delete view
* ✅ `get_object_or_404()`
* ✅ Delete confirmation page
* ✅ POST form
* ✅ CSRF protection
* ✅ Cancel navigation
* ✅ Separation between **showing confirmation** and **actually deleting**

And importantly:

> **No database record is deleted yet.**

### Next lesson

We'll handle the `POST` request and finally execute:

```python
student.delete()
```

Then we'll redirect back to the student list and complete the full CRUD cycle.
