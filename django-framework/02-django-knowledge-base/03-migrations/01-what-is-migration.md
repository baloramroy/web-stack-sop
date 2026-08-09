**Phase 3 — Migrations**

# Step 1: What is a Migration?

From the roadmap, we have already completed:

* ✅ Phase 1 — Build the Foundation
* ✅ Phase 2 — Models (`models.py`, creating the `Student` model)

So today we'll start **only the first topic** of Phase 3.

---

## Migration

Before typing any commands, you need to understand **why migrations exist**.

Many beginners memorize these commands:

```bash
python manage.py makemigrations
python manage.py migrate
```

without understanding what they actually do.

Our goal is to understand them first.

---

## Imagine This Scenario

Suppose your `Student` model looks like this:

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
```

This is **Python code**.

Your database, however, doesn't understand Python.

A database only understands things like:

```sql
CREATE TABLE student (
    id INTEGER,
    name VARCHAR(100),
    email VARCHAR(254),
    age INTEGER
);
```

So Django needs a way to convert your Python model into database instructions.

That's exactly what migrations are for.

---

## Think of It Like an Architect

Imagine you're building a house.

First, you draw the blueprint.

```
Blueprint
```

↓

Workers build the house.

```
Real House
```

In Django:

```
models.py
```

is the blueprint.

The database table is the real house.

A migration is the set of construction instructions that tells Django:

> "Create this table with these columns."

---

## Where Do Migrations Fit?

The flow now becomes:

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
      │
      ▼
Database Table
```

Notice something important:

**`models.py` does not change the database directly.**

There is an intermediate step.

That intermediate step is called a **migration**.

---

## Two Commands, Two Different Jobs

Many beginners think these commands do the same thing.

They do **different jobs**.

### Command 1

```bash
python manage.py makemigrations
```

Meaning:

> "Django, compare my models with the last known state and generate migration files."

It **does not** modify the database.

It only creates migration files.

#

### Command 2

```bash
python manage.py migrate
```

Meaning:

> "Execute all pending migration files and apply the changes to the database."

This command is what actually updates the database.

---

## A Real-Life Analogy

Suppose your manager says:

> "Build a new meeting room."

Step 1:

The architect creates the blueprint.

This is like:

```
makemigrations
```

Step 2:

The construction team builds the room.

This is like:

```
migrate
```

No blueprint → workers don't know what to build.

No workers → blueprint never becomes a real room.

Both steps are required.

---

## What Happens Internally?

When you run:

```bash
python manage.py makemigrations
```

Django:

1. Reads your `models.py`.
2. Compares it with previous migrations.
3. Detects what has changed.
4. Creates a new migration file.

When you later run:

```bash
python manage.py migrate
```

Django:

1. Reads the migration files.
2. Converts them into SQL.
3. Executes that SQL.
4. Updates the database schema.

---

## Important Concept

Your model is **not** your database.

```
models.py
        ≠
Database
```

They become synchronized **through migrations**.

---

## Lesson Summary

Today you learned:

* A model is only a Python representation of your data.
* Databases cannot understand Python models directly.
* **`makemigrations`** creates migration files based on model changes.
* **`migrate`** applies those migration files to the database.
* The database changes only after `migrate` is run.

---

## We intentionally did **not** run any commands today.

Just like in previous phases, we first build the concept. Once this is clear, the next lesson will be **Phase 3 → Step 2: Running `makemigrations`**, where we'll execute the command, examine the generated migration file, and understand exactly what Django creates before moving on to `migrate`. This follows the roadmap's sequence of learning `makemigrations`, then `migrate`, and finally checking the database. 
