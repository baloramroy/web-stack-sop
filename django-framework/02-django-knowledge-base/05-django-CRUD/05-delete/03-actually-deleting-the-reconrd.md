Exactly. This is the next lesson we identified:

> **Handle the POST request → delete the existing student → redirect to the student list.**

This completes the **Delete** operation and therefore completes the basic CRUD cycle.

# Phase 5 → CRUD → Delete

## Lesson: Actually Delete the Record

Our current view only handles the confirmation page:

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

The missing part is:

```text
POST
 ↓
student.delete()
 ↓
redirect
```

---

# Step 1 — Add the POST Check

Change the view to:

```python
def student_delete(request, id):

    student = get_object_or_404(
        Student,
        id=id
    )

    if request.method == "POST":

        student.delete()

        return redirect("student_list")

    return render(
        request,
        "myapp/student_delete.html",
        {
            "student": student
        }
    )
```

This is very similar to the Update view you just learned.

---

# Step 2 — Understand the Flow

When the user first visits:

```text
/students/2/delete/
```

the request is:

```text
GET
```

Therefore:

```python
if request.method == "POST":
```

is **false**.

Django continues to:

```python
return render(...)
```

and shows:

```text
Delete Student

Are you sure you want to delete:

ID: 2
Name: Alice
Email: alice@example.com
Age: 21

[ Yes, Delete ]

Cancel
```

Nothing has been deleted.

---

# Step 3 — User Clicks "Yes, Delete"

Our template already contains:

```html
<form method="POST">

    {% csrf_token %}

    <button type="submit">
        Yes, Delete
    </button>

</form>
```

When the user clicks the button, the browser sends:

```text
POST /students/2/delete/
```

Now Django enters:

```python
if request.method == "POST":
```

because the request method is `POST`.

---

# Step 4 — Delete the Student

Django executes:

```python
student.delete()
```

This is the key line.

It tells Django:

> Delete this existing model object from the database.

Suppose the database was:

| ID | Name  | Email                                         |
| -: | ----- | --------------------------------------------- |
|  1 | John  | [john@example.com](mailto:john@example.com)   |
|  2 | Alice | [alice@example.com](mailto:alice@example.com) |
|  3 | Bob   | [bob@example.com](mailto:bob@example.com)     |

Before:

```text
student = Alice
```

Then:

```python
student.delete()
```

Afterward:

| ID | Name | Email                                       |
| -: | ---- | ------------------------------------------- |
|  1 | John | [john@example.com](mailto:john@example.com) |
|  3 | Bob  | [bob@example.com](mailto:bob@example.com)   |

Alice's record has been removed.

---

# Step 5 — Redirect to the List

Immediately after deletion:

```python
return redirect("student_list")
```

This sends the user back to:

```text
/students/
```

So the complete process is:

```text
Click "Yes, Delete"
        │
        ▼
      POST
        │
        ▼
student.delete()
        │
        ▼
Database record removed
        │
        ▼
redirect("student_list")
        │
        ▼
Student List
```

---

# Why Do We Redirect?

We could technically render the student list directly after deleting.

But redirecting is the better pattern.

Remember the pattern from Update:

```text
POST
 ↓
Change database
 ↓
Redirect
 ↓
GET
 ↓
Display page
```

This is the **Post/Redirect/Get (PRG)** pattern.

It prevents the browser from remaining on the destructive POST request.

---

# Step 6 — Test It

Suppose you currently have:

```text
ID 1 → John
ID 2 → Alice
ID 3 → Bob
```

Open:

```text
/students/2/delete/
```

You should see:

```text
Delete Student

Are you sure you want to delete this student?

ID: 2
Name: Alice

[ Yes, Delete ]

Cancel
```

Click:

**Yes, Delete**

Django:

```text
POST
 ↓
student.delete()
 ↓
redirect("student_list")
```

You should arrive at:

```text
/students/
```

and now see:

```text
John
Bob
```

Alice should no longer appear.

---

# Verify the Database

This is important for learning.

Open the Django shell:

```bash
python manage.py shell
```

Then:

```python
from myapp.models import Student
```

Check:

```python
Student.objects.all()
```

You should no longer see the deleted student.

You can also check:

```python
Student.objects.filter(id=2).exists()
```

The result should be:

```python
False
```

Exit:

```python
exit()
```

---

# Complete Delete View

Your final Delete view is:

```python
from django.shortcuts import render, redirect, get_object_or_404
from .models import Student


def student_delete(request, id):

    student = get_object_or_404(
        Student,
        id=id
    )

    if request.method == "POST":

        student.delete()

        return redirect("student_list")

    return render(
        request,
        "myapp/student_delete.html",
        {
            "student": student
        }
    )
```

Notice how clean the logic is.

### GET

```text
Find student
 ↓
Show confirmation
```

### POST

```text
Find student
 ↓
Delete student
 ↓
Redirect
```

---

# One Important Detail

You might ask:

> Why do we retrieve the student before checking `POST`?

Because we need the object in both situations.

For GET:

```text
Need student information
→ show it on confirmation page
```

For POST:

```text
Need student object
→ delete it
```

That's why this comes first:

```python
student = get_object_or_404(
    Student,
    id=id
)
```

---

# 🎉 CRUD Is Now Complete

You've now implemented the basic CRUD cycle:

```text
             Django CRUD

        ┌──────────────────┐
        │     CREATE       │
        │                  │
        │ Create new row   │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │      READ        │
        │                  │
        │ List + Detail    │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │     UPDATE       │
        │                  │
        │ Modify row       │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │     DELETE       │
        │                  │
        │ Remove row       │
        └──────────────────┘
```

You now know the basic Django database workflow behind all four operations.

---

# Your CRUD Toolkit

| Operation           | Django Concept                   |
| ------------------- | -------------------------------- |
| Create              | `Student.objects.create()`       |
| Read List           | `Student.objects.all()`          |
| Read Detail         | `get_object_or_404()`            |
| Update              | Modify object + `student.save()` |
| Delete              | `student.delete()`               |
| Navigation          | `{% url %}`                      |
| Safe missing object | `get_object_or_404()`            |
| Data-changing forms | `POST` + `{% csrf_token %}`      |
| After POST          | `redirect()`                     |

---

## What Comes Next

**CRUD itself is now complete.** The next lessons should build on it rather than introducing another CRUD operation—for example, improving the CRUD pages with proper navigation and validation before moving forward in the roadmap.

We won't jump ahead until you've had a chance to test this Delete flow yourself.
