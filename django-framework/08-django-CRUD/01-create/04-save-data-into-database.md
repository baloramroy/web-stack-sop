**Phase 5 — CRUD: Create Operation**

# Lesson: Save the data into the database.

In the previous lesson, we learned:

* ✅ Display the form
* ✅ Submit the form using `POST`
* ✅ Read submitted data with `request.POST`

Now it's time to perform the final step of the **Create** operation:

---

## Today's Goal

When the user enters:

```text
Name : John
Email: john@example.com
Age  : 22
```

and clicks **Save**,

the flow becomes:

```text
Browser
     │
     ▼
Form
     │
     ▼
POST Request
     │
     ▼
student_create()
     │
     ▼
Student Model
     │
     ▼
Database
```

This is your **first complete CRUD Create operation**.

---

## Before We Write Code

Let's remember our `Student` model.

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
```

Every row in the database corresponds to one `Student` object.

For example:

| id | name | email                                       | age |
| -- | ---- | ------------------------------------------- | --- |
| 1  | John | [john@example.com](mailto:john@example.com) | 22  |

When we create a `Student` object in Django and save it, Django inserts a new row into the database.

---

## Step 1 — Import the Model

Open:

```text
views.py
```

Import the model:

```python
from django.shortcuts import render
from .models import Student
```

---

## Step 2 — Save the Student

Update your view:

```python
from django.shortcuts import render
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

    return render(request, "myapp/student_form.html")
```

---

## Understanding the New Code

This line:

```python
Student.objects.create(
```

asks Django to create a new `Student` object.

Think of it as saying:

> "Create a new student using the values I'm providing."

---

Here:

```python
name=name
```

The left side (`name`) is the field defined in the model.

The right side (`name`) is the variable we read from the submitted form.

The same applies to:

```python
email=email
age=age
```

---

## What Happens Internally?

Suppose the user submits:

```text
Name : John
Email: john@example.com
Age  : 22
```

Django receives:

```python
name = "John"
email = "john@example.com"
age = "22"
```

Then this code:

```python
Student.objects.create(
    name=name,
    email=email,
    age=age
)
```

becomes effectively:

```python
Student.objects.create(
    name="John",
    email="john@example.com",
    age="22"
)
```

Django translates this into an SQL `INSERT` statement behind the scenes and writes a new record to your database.

You don't have to write SQL manually.

---

## Step 3 — Test It

Start the server:

```bash
python manage.py runserver
```

Open:

```text
http://127.0.0.1:8000/students/add/
```

Enter:

```text
Name : Alice
Email: alice@example.com
Age  : 21
```

Click **Save**.

---

## Step 4 — Verify in Django Admin

Open the admin site:

```text
http://127.0.0.1:8000/admin/
```

Go to:

```text
Students
```

You should see a new record.

If you submit another student:

```text
Name : Bob
Email: bob@example.com
Age  : 24
```

you should now have two records.

This confirms that your Create operation is working.

---

## One Small Problem

After clicking **Save**, you'll notice that the same form page is displayed again.

If the user refreshes the page, the browser may ask:

> "Confirm Form Resubmission"

and clicking **Continue** can create a duplicate record.

This happens because after processing the POST request, we're rendering the same template instead of redirecting the user.

Our current flow is:

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
Render Same Template
```

This works, but it's not considered best practice.

---

## What We've Learned

Today you completed the essential Create operation:

```text
Browser
     │
     ▼
HTML Form
     │
     ▼
POST Request
     │
     ▼
request.POST
     │
     ▼
Student.objects.create()
     │
     ▼
Database
```

This is your first end-to-end CRUD operation in Django.

---

## Next Lesson

Before we move on to **Read (List)** as defined in the roadmap, we'll make one important improvement to the Create operation by following Django's standard **Post/Redirect/Get (PRG)** pattern. We'll redirect the user after saving to prevent duplicate submissions and make the workflow production-friendly. This is the final refinement of the Create operation before starting the next CRUD topic.
