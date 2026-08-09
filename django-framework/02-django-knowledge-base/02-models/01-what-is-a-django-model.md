**Phase 2 — Models**

# Step 1: What is a Django Model?

Today we will **not** create anything in the database.

We will only understand **what a Model is**.

---

## Think of a Real-Life Example

Imagine a school.

The school has many students.

Every student has information like:

* Name
* Email
* Age

If this were written on paper, it might look like this:

| Name  | Email                                         | Age |
| ----- | --------------------------------------------- | --- |
| Alice | [alice@example.com](mailto:alice@example.com) | 20  |
| Bob   | [bob@example.com](mailto:bob@example.com)     | 22  |

Now imagine storing this information digitally.

Django needs a way to describe **what information each student should have**.

That description is called a **Model**.

---

## What is a Model?

A **Model** is a Python class that describes the structure of data you want to store.

You can think of it like this:

> **A Model is the blueprint of a database table.**

It describes:

* What data will be stored
* What fields each record has
* The type of each field

It does **not** store the data itself.

---

## Real-Life Analogy

Imagine you are designing a paper form for student registration.

The form contains:

```
Student Registration Form

Name: ____________

Email: ___________

Age: _____________
```

Before anyone fills in the form, you first design the form itself.

That blank form is like a **Model**.

After people fill it in, each completed form becomes a **record** (we'll learn about records later).

---

## In Django

Every app contains a file named:

```text
myapp/
    models.py
```

This file is where Django expects you to define your data structure.

For our application, we'll create one model called:

```python
Student
```

---

## What Will Our Student Model Look Like?

Conceptually, our model will describe this information:

```
Student

├── name
├── email
└── age
```

Each student should have exactly these three pieces of information.

---

## Relationship to the Database

At this stage, **nothing exists in the database**.

The model is simply telling Django:

> "Whenever you create a table for students, it should contain these fields."

So the flow is:

```
models.py
      │
      ▼
Describe the data structure
      │
      ▼
Later...
      │
      ▼
Django creates the database table
```

Notice that the last step says **Later**. We are **not** creating the database table today. That happens in **Phase 3 (Migrations)**, exactly as your roadmap specifies. 

---

## Key Terms

| Term      | Meaning                                     |
| --------- | ------------------------------------------- |
| Model     | Blueprint describing data                   |
| Field     | One piece of information (name, email, age) |
| Record    | One row of data (we'll learn this later)    |
| models.py | File where models are defined               |

---

## Important Distinction

Many beginners think:

> Model = Database

This is **not** correct.

Instead:

```
Model
    │
    ▼
Description of the data
    │
    ▼
Later...
    │
    ▼
Database Table
```

The model comes **first**. The database table is generated from it later during migrations.

---

## Today's Goal

By the end of this lesson, you should be able to answer:

1. What is a Django Model?
2. Why do we use a Model?
3. What is a Field?
4. What is `models.py` used for?
5. Why is a Model called a blueprint?

---

## Next Lesson (Still Phase 2)

We'll write your **first `Student` model** inside `models.py` with these fields:

```python
name
email
age
```

We still **won't** create the database table or perform any CRUD operations. We'll stay consistent with the roadmap and leave database creation for **Phase 3 – Migrations**.
