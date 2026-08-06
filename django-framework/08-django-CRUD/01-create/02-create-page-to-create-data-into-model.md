 **Phase 5 — CRUD**

# Step 2: Create the page where users can add a new student

Notice something important:

> **Today we are only creating the page.**
>
> We are **NOT saving data to the database yet.**

This is the same learning style we've followed throughout the roadmap: understand one piece before combining everything.

---

## Our Goal Today

When you visit:

```text
http://127.0.0.1:8000/students/add/
```

You should see a page like this:

```text
Add Student

Name:
[________________]

Email:
[________________]

Age:
[________________]

        [ Save ]
```

The **Save** button will not work yet.

Today's objective is simply to display the form.

---

## Step 1 — Create a Template

Inside your app, create this folder structure if it doesn't already exist:

```text
myapp/
│
├── templates/
│   └── myapp/
│       └── student_form.html
```

Using `myapp/templates/myapp/` helps Django avoid template name conflicts when multiple apps have templates with the same filename.

---

## Step 2 — Create `student_form.html`

Add the following HTML:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Add Student</title>
</head>
<body>

    <h1>Add Student</h1>

    <form>

        <p>
            <label>Name</label><br>
            <input type="text" name="name">
        </p>

        <p>
            <label>Email</label><br>
            <input type="email" name="email">
        </p>

        <p>
            <label>Age</label><br>
            <input type="number" name="age">
        </p>

        <button type="submit">
            Save
        </button>

    </form>

</body>
</html>
```

At this point, it's just an HTML page.

There is **no Django form**, **no model**, and **no database interaction** yet.

---

## Step 3 — Create the View

Open:

```text
views.py
```

Add:

```python
from django.shortcuts import render

def student_create(request):
    return render(request, "myapp/student_form.html")
```

Let's understand this before moving on:

```python
def student_create(request):
```

This creates a Django view named `student_create`. Whenever a request reaches this view, Django executes the code inside it.

The `request` object contains information about the incoming HTTP request. Right now, we're not using it yet, but every Django view receives it.

---

Next line:

```python
return render(request, "myapp/student_form.html")
```

This tells Django:

1. Take the current request.
2. Find the template `myapp/student_form.html`.
3. Render it into HTML.
4. Send the HTML back to the browser.

This is exactly the request flow you learned in Phase 1:

```text
Browser
    │
    ▼
URL
    │
    ▼
View
    │
    ▼
Template
    │
    ▼
Browser
```

---

## Step 4 — Add a URL

### In your app's `urls.py`, add:

```python
from django.urls import path
from . import views

urlpatterns = [
    path("students/add/", views.student_create, name="student_create"),
]
```

This creates the route:

```text
/students/add/
```

When someone visits this URL, Django calls:

```python
views.student_create
```

#

### In your project's `urls.py`, add:

**Check your main project's `urls.py`**

```python
# myproject/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),  # This line must exist!
]
```

If you don't have this, the app's URLs won't be included.

#

### 📁 Final File Structure

```
myproject/
├── myproject/
│   └── urls.py           # ← Include the app's URLs here
├── myapp/
│   ├── templates/
│   │   └── myapp/
│   │       └── student_form.html
│   ├── urls.py           # ← Your new URL config
│   └── views.py          # ← Your new view
└── manage.py
```

---

## Step 5 — Run the Server

Start your development server:

```bash
python manage.py runserver
```

Open:

```text
http://127.0.0.1:8000/students/add/
```

You should now see your **Add Student** page with the three input fields and a Save button.

---

## What We Have Built

Here's the flow of today's lesson:

```text
Browser
      │
      ▼
/students/add/
      │
      ▼
urls.py
      │
      ▼
student_create()
      │
      ▼
student_form.html
      │
      ▼
Browser
```

Notice what is **missing**:

* ❌ No database
* ❌ No model saving
* ❌ No validation
* ❌ No Django forms
* ❌ No `POST` request handling

That's intentional. We're building the Create operation one layer at a time.

---

## Before We Move On

Please complete this page and make sure:

* ✅ The server starts without errors.
* ✅ Visiting `http://127.0.0.1:8000/students/add/` displays the form.
* ✅ You understand how the request flows from the URL to the view and then to the template.

Once that's working, we'll continue to the next step, where we'll make the **Save** button actually submit data to the Django view.
