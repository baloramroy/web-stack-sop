**Phase 3 — Migrations**

# Step 4: Check Your Database

We have completed:

* ✅ What migrations are
* ✅ `makemigrations`
* ✅ `migrate`

Now we'll complete the final roadmap item:

> **Then check your database.** 

This lesson is very important because **for the first time, you'll see how your Python code became a real database table.**

---

## Lesson Goal

By the end of this lesson, you'll understand:

* Where your data is stored.
* What tables Django created.
* What your `Student` table looks like.
* How `models.py` maps to the database.

---

## First, Which Database Are We Looking At?

In our roadmap, we've been learning with Django's default setup.

That means your project is currently using **SQLite** (unless you've already changed `settings.py` to MySQL).

So after running:

```bash
python manage.py migrate
```

you should have a file like this in your project root:

```text
myproject/
│
├── db.sqlite3
├── manage.py
├── myproject/
└── myapp/
```

Notice:

```text
db.sqlite3
```

This file **is your database**.

Think of it as a container that stores all your tables and data.

---

## What Is Inside `db.sqlite3`?

Many beginners imagine the database as one giant table.

It's not.

Instead, it contains **multiple tables**.

After your first migration, it looks conceptually like this:

```text
db.sqlite3
│
├── auth_user
├── auth_group
├── django_admin_log
├── django_session
├── django_content_type
├── django_migrations
│
└── myapp_student
```

Notice something:

Only **one** of these tables belongs to you.

The rest were created by Django itself.

---

## Why So Many Tables?

Let's identify them.

### Django Tables

```text
auth_user
```

Stores Django users.

#

```text
auth_group
```

Stores permission groups.

#

```text
django_session
```

Stores login sessions.

#

```text
django_admin_log
```

Stores actions performed in the Django Admin.

#

```text
django_migrations
```

Stores the history of applied migrations.

---

## Your Table

Since your model is:

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
```

Django creates a table for it.

By default, its name is:

```text
myapp_student
```

The pattern is:

```text
appname_modelname
```

Both names are lowercase.

So:

```text
myapp
+
Student
```

becomes:

```text
myapp_student
```

---

## What Does This Table Look Like?

Conceptually:

| id | name | email | age |
| -- | ---- | ----- | --- |
|    |      |       |     |

Right now, it has **no rows**.

Why?

Because we've only created the table.

We haven't inserted any data yet.

That will happen later in **Phase 4 (Admin)**.

---

## How Did Django Create These Columns?

Let's connect everything you've learned.

Your model:

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
```

became this database structure:

| Model Field | Database Column |
| ----------- | --------------- |
| `name`      | `name`          |
| `email`     | `email`         |
| `age`       | `age`           |

Notice something interesting.

You never wrote:

```sql
CREATE TABLE
```

You never wrote:

```sql
VARCHAR
```

You never wrote SQL at all.

Django translated your model into the appropriate database schema.

---

## Where Did the `id` Column Come From?

Look at your model again.

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
```

Do you see an `id` field?

No.

Yet the table has one.

Why?

Because Django automatically adds a primary key field if you don't define one yourself.

So your database table is actually more like:

| id | name | email | age |
| -- | ---- | ----- | --- |

This `id` uniquely identifies every record.

We'll learn more about primary keys later, so don't worry about the details yet.

---

## The Complete Journey

Let's put all of Phase 3 together.

```text
You write a model
        │
        ▼
models.py
        │
        ▼
python manage.py makemigrations
        │
        ▼
0001_initial.py
        │
        ▼
python manage.py migrate
        │
        ▼
Database Table Created
        │
        ▼
db.sqlite3
        │
        ▼
myapp_student
```

This is the complete lifecycle of a new model.

---

## What We Have Achieved So Far

Let's look back at everything you've built.

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
Model
    │
    ▼
Migration
    │
    ▼
Database
```

This is a major milestone. You've gone from understanding how a request reaches your code to creating a real database table.

---

## Common Beginner Questions

### "Can I open `db.sqlite3` in a text editor?"

No.

It's a binary database file, not a plain text file.

To inspect it, you use database tools (such as DB Browser for SQLite) or Django itself.

#

### "Why is my `Student` table empty?"

Because creating a table and inserting data are different operations.

So far you've only created the table structure.

We'll start adding records in **Phase 4 — Django Admin**.

#

### "Do I need to create the table manually?"

No.

That's one of Django's biggest advantages.

You define the model, generate a migration, and apply it. Django handles the SQL and table creation for you.

#

## Phase 3 Summary

You now understand the complete migration workflow:

1. Write a model in `models.py`.
2. Run `python manage.py makemigrations` to generate migration files.
3. Run `python manage.py migrate` to apply those migrations.
4. Verify that the database now contains your new table.

This completes **Phase 3** exactly as defined in our roadmap. 

---

## Next Phase

In our next lesson, we'll begin **Phase 4 — Django Admin**.

According to the roadmap, we'll start with the first step:

> **Register the model. Create some records from the Admin panel. No code yet.** 

We'll go slowly and first understand **what the Django Admin is and why Django includes it**, before we write any code.
