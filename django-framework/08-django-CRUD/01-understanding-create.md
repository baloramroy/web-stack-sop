**Phase 5 — CRUD**

# Lesson 1: Understanding "Create"

Today we will **not write code immediately**.

First, you need to understand what **Create** actually means.

CRUD stands for:

| Letter | Meaning |
| ------ | ------- |
| C      | Create  |
| R      | Read    |
| U      | Update  |
| D      | Delete  |

We'll only learn **C = Create** today.

---

## What does "Create" mean?

Imagine your `Student` model from the previous phases.

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
```

The database is currently empty.

Suppose a user enters:

```
Name : John
Email: john@example.com
Age  : 22
```

After clicking **Save**, Django inserts a new row into the database.

Before:

| ID        | Name | Email | Age |
| --------- | ---- | ----- | --- |
| *(empty)* |      |       |     |

After:

| ID | Name | Email                                       | Age |
| -- | ---- | ------------------------------------------- | --- |
| 1  | John | [john@example.com](mailto:john@example.com) | 22  |

That entire process is called **Create**.

---

## In a Django application

The Create operation usually involves these parts:

```
Browser
     │
     ▼
Form
     │
     ▼
View
     │
     ▼
Model
     │
     ▼
Database
```

Each part has a specific responsibility.

### 1. Browser

The user opens a page.

Example:

```
http://127.0.0.1:8000/students/add/
```

#

### 2. Form

The page displays input fields.

```
Name
Email
Age

[ Save ]
```

The user fills in the information.

#

### 3. View

When the user clicks **Save**, the request goes to a Django view.

The view is responsible for things like:

* Receiving the submitted data
* Validating it
* Creating a new model object
* Saving it to the database
* Returning a response

Think of the view as the coordinator between the browser and the database.

#

### 4. Model

The model defines what a student looks like.

It knows:

* which fields exist,
* what data types they have,
* and how to save them to the database.

#

### 5. Database

Finally, Django stores the new record in the database.

---

## The complete flow

```
User opens page
        │
        ▼
Student Form
        │
User enters data
        │
Clicks Save
        │
        ▼
Django View
        │
Creates Student object
        │
        ▼
Database
        │
Student saved
        │
        ▼
Response returned to browser
```

This is the complete lifecycle of a basic **Create** operation.

---

## Why are we learning this first?

If you understand this flow, every Create operation in Django—whether it's for students, employees, servers, inventory, or any other model—follows the same pattern. The model changes, but the overall process remains the same.

---

## Today's Goal

By the end of this lesson, you should be able to answer:

* ✅ What does CRUD stand for?
* ✅ What does **Create** mean?
* ✅ Which components participate in creating a new record?
* ✅ What is the flow from browser to database?

---

## Next Lesson (Phase 5 → Step 2)

We will start writing code for the Create operation by creating the page where users can add a new student. We'll build it one small piece at a time, maintaining the same slow, step-by-step approach defined in your roadmap.
