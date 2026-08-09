**Phase 4 — Django Admin**

# Lesson 3: Create Your First Django Superuser

**Goal of this lesson:**

Create an administrator account that can log into the Django Admin panel.

We will **not** create any `Student` records yet. Today we're only creating the account that has permission to access the Admin site.

---

## What is a Superuser?

A **superuser** is a special user with **all permissions** in your Django project.

A superuser can:

* View all registered models
* Add records
* Edit records
* Delete records
* Create other users
* Manage permissions

Think of it as the "Administrator" account of your application.

---

## Where is the Superuser Stored?

A common question is:

> "If I create a superuser, where does Django save it?"

The answer is:

**In your database.**

When you ran migrations in Phase 3, Django created several built-in tables.

One of them is for authentication.

```text
Database
│
├── Student
├── django_migrations
├── django_content_type
├── django_session
└── auth_user
```

When you create a superuser, Django inserts a new row into:

```text
auth_user
```

Your `Student` model and the superuser are **completely separate**.

```text
Student Model
        │
        ▼
 Student Table


Superuser
        │
        ▼
 auth_user Table
```

---

## Step 1 — Open the Terminal

Open a terminal in the folder where `manage.py` is located.

Example:

```text
myproject/
│
├── manage.py
├── myproject/
└── myapp/
```

You should be in the directory that contains:

```text
manage.py
```

---

## Step 2 — Activate Your Virtual Environment

If it isn't already active, activate it.

### Windows

```bash
venv\Scripts\activate
```

### Linux/macOS

```bash
source venv/bin/activate
```

Your prompt should now indicate that the virtual environment is active.

---

## Step 3 — Run the Command

Execute:

```bash
python manage.py createsuperuser
```

Django will start an interactive setup.

Example:

```text
Username: admin
Email address: admin@example.com
Password:
Password (again):
```

---

## Step 4 — Choose a Username

Example:

```text
Username: admin
```

You can choose any username you like.

Examples:

```text
admin
baloram
administrator
```

---

## Step 5 — Enter an Email

Example:

```text
Email address: admin@example.com
```

The email is optional by default, but it's good practice to provide one.

---

## Step 6 — Enter a Password

You'll be prompted twice:

```text
Password:
Password (again):
```

As you type, **nothing will appear on the screen**.

No `*`
No dots
No characters

This is normal terminal behavior for password input.

---

## Step 7 — Password Validation

If your password is weak, Django may display a warning such as:

```text
This password is too short.
This password is too common.
```

You'll then be asked something like:

```text
Bypass password validation and create user anyway? [y/N]
```

For learning purposes, you can choose a stronger password instead of bypassing the validation.

---

## Step 8 — Success

If everything is successful, you'll see:

```text
Superuser created successfully.
```

At this point:

* Your administrator account exists.
* It has been saved in the `auth_user` table.
* It can now be used to log into the Django Admin site.

---

## What Happens Internally?

Here's the complete flow:

```text
You
 │
 ▼
python manage.py createsuperuser
 │
 ▼
Django Authentication System
 │
 ▼
Validates your input
 │
 ▼
Hashes your password
 │
 ▼
Stores the user in auth_user
```

Notice an important point:

**Django does not store your password as plain text.**

Instead, it stores a **hashed** version of the password. This is a one-way transformation that improves security. When you log in later, Django hashes the password you enter and compares it with the stored hash.

---

## Did We Write Any Code?

**No.**

In this lesson:

* ❌ We didn't modify `views.py`.
* ❌ We didn't modify `models.py`.
* ❌ We didn't modify `admin.py`.
* ❌ We didn't create templates.

We only used Django's built-in management command to create an administrator account.

---

## Lesson Summary

Today you learned:

* ✅ What a Django superuser is.
* ✅ A superuser has full administrative permissions.
* ✅ Superusers are stored in Django's built-in `auth_user` table.
* ✅ The `createsuperuser` command creates the account interactively.
* ✅ Django securely stores a hashed password instead of the plain-text password.

---

## Practical Exercise

1. Open your project directory.
2. Activate your virtual environment.
3. Run:

```bash
python manage.py createsuperuser
```

4. Create your administrator account.
5. Confirm you see:

```text
Superuser created successfully.
```

Once you've done that, we'll move to **Phase 4 → Lesson 4: Log into the Django Admin Panel and verify that your registered `Student` model appears**, exactly following the roadmap. 
