**Phase 4 — Django Admin**

# Lesson 1: What is Django Admin?

## Purposes

Before writing anything, understand **why Django Admin exists**.

Think of Django as having **two different websites**.

```
Website 1
(User-facing website)

http://127.0.0.1:8000/
```

This is the website your users will use.

Example:

* Home
* About
* Contact
* Products
* Blog

---

The second website is built automatically by Django.

```
Website 2
(Admin website)

http://127.0.0.1:8000/admin/
```

This is **not** for customers.

It is for:

* Administrator
* Staff
* Content manager
* Developer (during development)

---

## Why does Django provide an Admin Panel?

Imagine you have a `Student` model.

Instead of writing pages like:

* Add Student
* Edit Student
* Delete Student
* View Students

Django already provides an interface where you can do these operations.

So during development you can quickly manage your data.

---

## Think of it like this

Suppose your model is:

```
Student
```

Without Django Admin:

```
You must build

Add Student page

Edit Student page

Delete Student page

List Student page
```

With Django Admin:

```
Django already provides all of them.

You only need to tell Django:

"This model should appear in the admin."
```

---

## Where does Django Admin get its data?

Everything comes from your **models**.

```
Model
   │
   ▼
Database
   │
   ▼
Django Admin
```

The Admin panel doesn't store separate data.

It simply reads and writes records in your database through your models.

---

## Visual Flow

```
            models.py
                 │
                 ▼
            Database
                 │
                 ▼
          Django Admin
                 │
                 ▼
        Add / Edit / Delete
```

---

## Is Django Admin meant for public users?

**No.**

Normally:

| Public Website | Django Admin          |
| -------------- | --------------------- |
| Customers      | Administrators        |
| Visitors       | Staff                 |
| Everyone       | Authorized users only |

The Admin site is protected by login credentials.

---

## In a Real Company

Imagine you work on an HR Management System.

Employees visit:

```
company.com
```

HR administrators log into:

```
company.com/admin/
```

There they can:

* Add employees
* Update employee details
* Remove records
* Manage departments

The employees never use the Admin panel directly.

---

## What We Will Do in This Phase

Following the roadmap, we will only learn:

1. Understand what Django Admin is. ✅ (Today's lesson)
2. Register the `Student` model.
3. Create a Superuser.
4. Log into the Admin panel.
5. Create Student records from the Admin interface.

We will **not** cover:

* Custom Admin pages
* Custom forms
* Search fields
* Filters
* List display
* Inline models
* Admin customization

Those topics belong later, after you've built a solid foundation.

---

## Lesson Summary

By the end of today's lesson, you should understand:

* ✅ Django Admin is a built-in administration website.
* ✅ It is intended for administrators and staff, not end users.
* ✅ It works directly with your Django models and database.
* ✅ It allows you to manage data without building CRUD pages yourself.
* ✅ In this phase, we'll use it only to create and manage records, keeping with the roadmap. 

---

## Next Lesson (Phase 4 → Lesson 2)

We'll take the first practical step:

> **Register the `Student` model with Django Admin**

This is the step that makes your model appear in the Admin panel for the first time.
