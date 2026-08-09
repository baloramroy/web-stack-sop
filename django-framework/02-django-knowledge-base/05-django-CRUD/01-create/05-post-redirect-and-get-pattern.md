**Phase 5 — CRUD: Create Operation**

# Lesson: Post/Redirect/Get (PRG) Pattern


## Why Do We Need This?

Suppose a user fills out the form:

```text
Name : John
Email: john@example.com
Age  : 22
```

Clicks **Save**.

The student is saved successfully.

Now the user presses **F5** (Refresh).

The browser displays:

```text
Confirm Form Resubmission

To display this page, the browser needs to resend the information
that was previously submitted.
```

If the user clicks **Continue**...

The form is submitted **again**.

Now your database becomes:

| ID | Name | Email                                       | Age |
| -- | ---- | ------------------------------------------- | --- |
| 1  | John | [john@example.com](mailto:john@example.com) | 22  |
| 2  | John | [john@example.com](mailto:john@example.com) | 22  |

You accidentally created a duplicate record.

---

## Why Does This Happen?

Our current code is:

```python
def student_create(request):

    if request.method == "POST":

        name = request.POST.get("name")
        email = request.POST.get("email")
        age = request.POST.get("age")

        Student.objects.create(
            name=name,
            email=email,
            age=age
        )

    return render(request, "myapp/student_form.html")
```

Notice the last line:

```python
return render(request, "myapp/student_form.html")
```

Even after saving, Django returns the page as the response to the **POST** request.

The browser remembers:

> "The current page came from a POST request."

Refreshing means repeating that POST request.

---

## The Better Solution

Instead of rendering immediately after saving, we redirect the user.

The flow becomes:

```text
Browser
     │
POST
     │
     ▼
View
     │
Save Student
     │
     ▼
Redirect
     │
     ▼
GET Request
     │
     ▼
Display Form
```

The browser's current page is now the result of a **GET** request.

Refreshing simply repeats the GET request, not the POST.

No duplicate records are created.

---

## Step 1 — Import `redirect`

Open `views.py`:

```python
from django.shortcuts import render, redirect
from .models import Student
```

---

## Step 2 — Update the View

Replace the view with:

```python
from django.shortcuts import render, redirect
from .models import Student

def student_create(request):

    if request.method == "POST":

        name = request.POST.get("name")
        email = request.POST.get("email")
        age = request.POST.get("age")

        Student.objects.create(
            name=name,
            email=email,
            age=age
        )

        return redirect("student_create")

    return render(request, "myapp/student_form.html")
```

---

## Understanding `redirect()`

This line:

```python
return redirect("student_create")
```

does **not** render HTML.

Instead, Django tells the browser:

> "Go to another URL."

Because `"student_create"` is the name of the URL pattern:

```python
path(
    "students/add/",
    views.student_create,
    name="student_create"
)
```

Django finds the correct URL and sends the browser there.

---

## What Actually Happens?

### Before (Old Flow)

```text
GET /students/add/
        │
        ▼
Show Form
        │
User submits
        │
        ▼
POST /students/add/
        │
        ▼
Save Student
        │
        ▼
Render Form Again
```

The browser is still on a POST response.

#

### After (PRG Flow)

```text
GET /students/add/
        │
        ▼
Show Form
        │
User submits
        │
        ▼
POST /students/add/
        │
        ▼
Save Student
        │
        ▼
Redirect
        │
        ▼
GET /students/add/
        │
        ▼
Show Empty Form
```

Now the browser is on a GET response.

Refreshing the page is completely safe.

---

## Why Use the URL Name?

You might wonder why we wrote:

```python
redirect("student_create")
```

instead of:

```python
redirect("/students/add/")
```

Using the URL **name** is the Django best practice.

Imagine that six months later you change the URL:

From:

```text
/students/add/
```

To:

```text
/student/create/
```

You only need to update `urls.py`.

Every `redirect("student_create")` will continue to work automatically because the URL name hasn't changed.

---

## Test It

1. Run the server:

```bash
python manage.py runserver
```

2. Open:

```text
http://127.0.0.1:8000/students/add/
```

3. Add a student.

4. Click **Save**.

You should notice:

* The form reloads with empty fields.
* There is **no browser warning** if you press **F5**.
* Refreshing the page **does not create another student**.

---

## What We Learned Today

You learned the **Post/Redirect/Get (PRG)** pattern:

```text
Browser
     │
GET
     │
     ▼
Show Form
     │
POST
     │
     ▼
Save to Database
     │
Redirect
     │
     ▼
GET
     │
     ▼
Show Form Again
```

This is the standard pattern you'll see in Django applications because it prevents duplicate form submissions and gives users a smoother experience.

---

## 🎉 Phase 5 — Create Completed

You have now completed the **Create** part of CRUD:

* ✅ Display a form
* ✅ Submit data with `POST`
* ✅ Read data from `request.POST`
* ✅ Save a model using `Student.objects.create()`
* ✅ Redirect after saving using the PRG pattern

This completes the first CRUD operation from your roadmap.

---

## Next Lesson

We'll begin the next CRUD topic from the roadmap:

> **Read (List)**

You'll learn how to retrieve **all students** from the database and display them in an HTML table, introducing Django's querying with `Student.objects.all()`.
