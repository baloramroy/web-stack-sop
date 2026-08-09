**Phase 3 — Migrations**

# Step 2: Running `makemigrations`

## Lesson Goal

By the end of this lesson, you'll be able to answer:

* What does `makemigrations` actually do?
* What files does it create?
* Where are those files stored?
* Why are they important?

---

## Before We Begin

Let's assume your project structure looks like this:

```text
myproject/
│
├── manage.py
│
├── myproject/
│
└── myapp/
    ├── migrations/
    │   └── __init__.py
    ├── models.py
    └── ...
```

And your `Student` model is:

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
```

Notice the `migrations` folder.

Right now it contains only:

```text
__init__.py
```

There are **no migration files yet**.

---

## Step 1 — Save Your Model

Before creating a migration:

* Write your model.
* Save `models.py`.

Django always reads the **saved** version of your model.

If you forget to save the file, Django won't detect your changes.

---

## Step 2 — Run the Command

From the directory containing `manage.py`, run:

```bash
python manage.py makemigrations
```

If everything is correct, Django will display something similar to:

```text
Migrations for 'myapp':
  myapp/migrations/0001_initial.py
    + Create model Student
```

Don't worry if the formatting is slightly different. The important part is understanding what Django is telling you.

Let's break it down.

#

### `Migrations for 'myapp':`

```text
Migrations for 'myapp':
```

Django detected changes in the **myapp** application.

If you had multiple apps, Django would report changes separately for each one.

#

### `0001_initial.py`

```text
0001_initial.py
```

This is the **first migration** for your app.

Let's decode the name:

```
0001
```

means:

> This is migration number 1.

```
initial
```

means:

> This migration creates the initial database structure for this app.

#

### `Create model Student`

```text
+ Create model Student
```

Django has detected that your `Student` model doesn't exist in the database history yet.

So it plans to create it.

Notice the wording:

It says **plans**.

It does **not** say it has already created the table.

Nothing has been written to the database yet.

---

## What Changed?

Before running the command:

```text
migrations/

└── __init__.py
```

After running:

```text
migrations/

├── __init__.py
└── 0001_initial.py
```

A new Python file has appeared.

---

## Is It Really a Python File?

Yes.

Open:

```text
myapp/migrations/0001_initial.py
```

You'll see something similar to:

```python
from django.db import migrations, models

class Migration(migrations.Migration):

    initial = True

    dependencies = []

    operations = [
        migrations.CreateModel(
            name="Student",
            fields=[
                ("id", models.BigAutoField(...)),
                ("name", models.CharField(max_length=100)),
                ("email", models.EmailField(max_length=254)),
                ("age", models.IntegerField()),
            ],
        ),
    ]
```

Don't worry about every line yet.

Focus on what this file represents.

---

## What Is This File?

This file is **a set of instructions**.

It's Django saying:

> "When someone runs `migrate`, create a table named `Student` with these fields."

Think of it as a construction plan.

It doesn't build anything by itself.

It simply records **what needs to be built**.

---

## Has the Database Changed?

**No.**

At this point:

```text
models.py
        │
        ▼
0001_initial.py
```

The database is still unchanged.

You have only created the migration file.

This is one of the most important concepts in Django.

---

## Why Doesn't `makemigrations` Change the Database?

Imagine you accidentally make a mistake in your model.

If Django modified the database immediately, fixing mistakes would be much harder.

Instead, Django separates the process into two steps:

1. Generate migration instructions (`makemigrations`)
2. Apply those instructions (`migrate`)

This gives you a chance to inspect the migration before any database changes occur.

---

## Where Does Django Know What Changed?

When you run `makemigrations`, Django:

1. Reads your current `models.py`.
2. Compares it with the previous migration history.
3. Detects differences.
4. Creates a new migration file describing only those differences.

That's why Django doesn't recreate everything every time—it only records what's new or changed.

---

## Common Beginner Mistakes

### Mistake 1: Forgetting to save `models.py`

If you don't save the file before running `makemigrations`, Django won't see your latest changes.

#

### Mistake 2: Expecting a database table immediately

Running:

```bash
python manage.py makemigrations
```

does **not** create any tables.

It only creates migration files.

#

### Mistake 3: Editing migration files manually

As a beginner, avoid editing files inside the `migrations` folder.

Let Django generate them for you.

Later in your Django journey, you'll learn when and how to customize migrations safely.

---

## Visual Flow

```
You write a model
        │
        ▼
models.py
        │
        ▼
python manage.py makemigrations
        │
        ▼
0001_initial.py created
        │
        ▼
Database
    (No change yet)
```

---

## Lesson Summary

Today you learned:

* How to run `python manage.py makemigrations`
* Why Django creates a `0001_initial.py` file
* That migration files are Python files containing database change instructions
* That **`makemigrations` never modifies the database**
* That the database will remain unchanged until `migrate` is executed

---

## Next Lesson

In the next lesson, we'll learn **Phase 3 → Step 3: `python manage.py migrate`**.

There, we'll see how Django reads the migration file, executes it, creates the actual database tables, and then we'll inspect the database to verify that the `Student` table has been created. This completes the roadmap's sequence of **`makemigrations` → `migrate` → check the database**. 
