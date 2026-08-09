**Phase 3 — Migrations**

# Step 3: `migrate`

We have now completed:

* ✅ Phase 1 — Foundation
* ✅ Phase 2 — Models
* ✅ Phase 3 → Step 1: What are Migrations?
* ✅ Phase 3 → Step 2: `makemigrations`

---

## Lesson Goal

By the end of this lesson, you'll understand:

* What `migrate` actually does.
* What happens internally.
* Why migration files are needed.
* What Django creates in the database.

---

## Where We Left Off

After running:

```bash
python manage.py makemigrations
```

our situation looked like this:

```
models.py
      │
      ▼
0001_initial.py
      │
      ▼
Database
(No changes yet)
```

The migration file exists.

The database has **not** changed.

Now comes the second step.

---

## Run the Command

From the directory containing `manage.py`, run:

```bash
python manage.py migrate
```

You should see output similar to:

```text
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions, myapp

Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying sessions.0001_initial... OK
  Applying myapp.0001_initial... OK
```

Let's understand every part.

---

## What Does "Apply all migrations" Mean?

```
Apply all migrations:
```

Remember:

The `migrations` folder contains instructions.

When you run `migrate`, Django goes through every unapplied migration and executes it.

Think of it like this:

```
Migration File
        │
        ▼
Read Instructions
        │
        ▼
Generate SQL
        │
        ▼
Execute SQL
        │
        ▼
Database Updated
```

---

## Why Are There So Many Apps?

You might notice migrations for:

```
admin

auth

contenttypes

sessions
```

and wonder:

> "I only created the Student model. Why is Django migrating all these apps?"

Because Django comes with several built-in applications.

For example:

### `auth`

Handles:

* Users
* Passwords
* Groups
* Permissions

#

### `admin`

Provides the Django Admin interface.

#

### `sessions`

Stores user session information.

#

### `contenttypes`

Allows Django to understand relationships between different models internally.

#

These built-in apps also need database tables.

So the first time you run `migrate`, Django creates tables for both:

* Django's built-in apps
* Your own app (`myapp`)

---

## What Happens Internally?

Let's go step by step.

### Step 1

Django finds:

```
myapp/migrations/0001_initial.py
```

#

### Step 2

It reads the instructions inside:

```python
migrations.CreateModel(
    name="Student",
    ...
)
```

#

### Step 3

Django converts those instructions into SQL.

Conceptually, it becomes something like:

```sql
CREATE TABLE student (
    id INTEGER PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(254),
    age INTEGER
);
```

You don't write this SQL yourself—Django generates it for you.

#

### Step 4

The database executes the SQL.

Now the table actually exists.

This is the first time your database changes.

---

## Visual Flow

```
models.py
      │
      ▼
makemigrations
      │
      ▼
0001_initial.py
      │
      ▼
migrate
      │
      ▼
SQL Generated
      │
      ▼
Database Table Created
```

---

## What Changed?

Before `migrate`:

```
Database

(No Student table)
```

After `migrate`:

```
Database

Student
--------
id
name
email
age
```

This is the actual table stored in your database.

---

## Does Django Remember This?

Yes.

A common beginner question is:

> "If I run `migrate` again, will Django recreate all the tables?"

The answer is **No**.

Django keeps track of applied migrations in a special table called:

```
django_migrations
```

This table records which migration files have already been applied.

For example:

```
django_migrations

-----------------------------------------
app           migration
-----------------------------------------
auth          0001_initial
admin         0001_initial
myapp         0001_initial
sessions      0001_initial
```

The next time you run:

```bash
python manage.py migrate
```

Django checks this table first.

If a migration has already been applied, it skips it.

---

## What If I Run `migrate` Again?

You'll usually see something like:

```text
Operations to perform:
  Apply all migrations

No migrations to apply.
```

That means:

* Django checked the `django_migrations` table.
* Everything is already up to date.
* No database changes were needed.

---

## Common Beginner Mistakes

### Mistake 1: Forgetting `makemigrations`

If you change `models.py` and immediately run:

```bash
python manage.py migrate
```

without creating a new migration, Django has no new instructions to apply.

#

### Mistake 2: Thinking `migrate` reads `models.py`

It doesn't.

`migrate` reads **migration files**, not your models directly.

The flow is always:

```
models.py
      │
      ▼
makemigrations
      │
      ▼
Migration File
      │
      ▼
migrate
```

#

### Mistake 3: Deleting migration files after applying them

Once a migration has been applied, deleting its file can lead to inconsistencies between your project and the database.

As a beginner, let Django manage the migration files.

---

## Summary

Today you learned:

* `python manage.py migrate` applies pending migrations.
* Django reads migration files, not `models.py`, during this step.
* Migration instructions are converted into SQL and executed.
* Your `Student` table is created only after `migrate` runs.
* Django records applied migrations in the `django_migrations` table, preventing the same migration from running twice.

---

## Next Lesson

According to the roadmap, the final part of **Phase 3** is:

> **Check your database.** 

In the next lesson, we'll inspect the database after running `migrate`. We'll see the tables Django created, identify your `Student` table, and connect what you wrote in `models.py` to the actual database structure. We'll do this slowly, just as we've done in every previous phase.
