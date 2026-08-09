**Phase 4 — Django Admin**

## Lesson 4: Log into the Django Admin Panel

**Goal of this lesson:**

* Start the Django development server.
* Open the Django Admin site.
* Log in using your superuser account.
* Verify that the `Student` model appears in the Admin panel.

We will **not** create any student records yet. That will be the next lesson.

---

## Step 1 — Make Sure You Have Completed the Previous Lessons

Before continuing, you should have:

* ✅ Created the `Student` model.
* ✅ Run `makemigrations` and `migrate`.
* ✅ Registered the model in `admin.py`.
* ✅ Created a superuser.

Without these, this lesson won't work as expected.

---

## Step 2 — Start the Development Server

Open a terminal in the directory containing `manage.py`.

Run:

```bash
python manage.py runserver
```

If everything is working, you'll see output similar to:

```text
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.
```

The important part is:

```text
http://127.0.0.1:8000/
```

This means your Django application is running.

---

## Step 3 — Open the Admin URL

Open your web browser and visit:

```text
http://127.0.0.1:8000/admin/
```

Notice something important.

Earlier in Phase 1, you visited:

```text
http://127.0.0.1:8000/
```

Now you're visiting:

```text
http://127.0.0.1:8000/admin/
```

The `/admin/` path is already configured by Django when you create a new project.

---

## Step 4 — Why Does `/admin/` Work?

Open your project's `urls.py`.

You should already have something like this:

```python
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path("admin/", admin.site.urls),
]
```

Let's understand this line:

```python
path("admin/", admin.site.urls)
```

Break it into two parts.

### Part 1

```python
"admin/"
```

This is the URL.

When someone visits:

```text
http://127.0.0.1:8000/admin/
```

Django matches this URL.

#

### Part 2

```python
admin.site.urls
```

This tells Django:

> "Use Django's built-in Admin application for everything under `/admin/`."

Unlike your own app, you didn't write these views. Django provides them for you.

---

## Visual Flow

```text
Browser
    │
    ▼
/admin/
    │
    ▼
Project urls.py
    │
    ▼
admin.site.urls
    │
    ▼
Django Admin Application
    │
    ▼
Login Page
```

---

## Step 5 — The Login Page

When you first visit `/admin/`, you'll see a login screen.

It asks for:

```text
Username

Password
```

Use the superuser credentials you created in the previous lesson.

Example:

```text
Username: admin
Password: ********
```

---

## Step 6 — What Happens After You Click "Log in"?

Django checks:

```text
Did this user exist?

↓

Is the password correct?

↓

Is the user active?

↓

Is the user allowed to access the Admin?
```

If all checks pass:

```text
Login Successful
```

If not:

```text
Please enter the correct username and password.
```

---

## Step 7 — The Admin Home Page

After logging in, you'll see the Django Admin dashboard.

Because you registered the `Student` model earlier, it should now appear under your app.

A simplified view might look like:

```text
Myapp
 └── Students
```

This confirms that:

* Django found your `Student` model.
* The model was successfully registered in `admin.py`.
* The Admin site is ready to manage `Student` records.

---

## How Did `Student` Get Here?

Let's trace the flow:

```text
Student Model
      │
      ▼
admin.py
      │
      ▼
admin.site.register(Student)
      │
      ▼
Django Admin
      │
      ▼
Student appears on the Admin dashboard
```

Notice that you didn't create any HTML page for this. Django generated the interface automatically.

---

## Common Problems

### Problem 1: `Student` Doesn't Appear

Check that you have:

```python
from .models import Student

admin.site.register(Student)
```

in `admin.py`.

#

### Problem 2: "Please enter the correct username and password."

Possible causes:

* Wrong username
* Wrong password
* Superuser wasn't created

You can create another superuser with:

```bash
python manage.py createsuperuser
```

#

### Problem 3: Page Not Found (404)

Make sure your project's `urls.py` contains:

```python
path("admin/", admin.site.urls),
```

#

### Problem 4: Server Isn't Running

Start it again:

```bash
python manage.py runserver
```

---

## What We Have Accomplished

At this point, your project has:

```text
Project
    │
    ▼
App
    │
    ▼
Student Model
    │
    ▼
Database
    │
    ▼
Registered in Admin
    │
    ▼
Visible in Admin Panel
```

You now have a complete path from your model to the Admin interface.

---

## Lesson Summary

Today you learned:

* ✅ How to start the Django development server.
* ✅ Why `http://127.0.0.1:8000/admin/` works.
* ✅ The role of `path("admin/", admin.site.urls)` in the project's `urls.py`.
* ✅ How to log in with a superuser.
* ✅ How to verify that the registered `Student` model appears in the Admin dashboard.

---

## Next Lesson (Phase 4 → Lesson 5)

We'll complete the final step of this phase:

> **Create your first `Student` records from the Django Admin panel.**

This will be the first time you insert data into your `Student` table without writing any CRUD views, exactly as your roadmap specifies.
