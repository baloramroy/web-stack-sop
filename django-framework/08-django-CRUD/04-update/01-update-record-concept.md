**Phase 5 → CRUD → Update**

# Lesson 1: What is an Update?

As always, we'll go **one small step at a time**. Today we will **not update the database yet**. First, we'll understand what an update operation is and why it starts with a pre-filled form.

Suppose your database contains this record:

| ID | Name | Email                                       | Age |
| -- | ---- | ------------------------------------------- | --- |
| 1  | John | [john@example.com](mailto:john@example.com) | 22  |

Later, John changes his email address.

The database should become:

| ID | Name | Email                                                   | Age |
| -- | ---- | ------------------------------------------------------- | --- |
| 1  | John | [john.smith@example.com](mailto:john.smith@example.com) | 22  |

Notice something important.

The **student is still the same person**.

Only one field changed.

We are **not creating another student**.

---

## Create vs Update

Let's compare them.

### Create

The form starts empty.

```text
Name:
[____________]

Email:
[____________]

Age:
[____________]
```

The user enters new information.

After clicking **Save**, Django creates a **new row**.

#

### Update

The form is already filled in.

```text
Name:
[John________]

Email:
[john@example.com]

Age:
[22__________]
```

The user edits one or more fields.

```text
Email:
[john.smith@example.com]
```

After clicking **Save**, Django **updates the existing row**.

No new student is created.

---

## The Biggest Difference

Create:

```text
Empty Form
      │
      ▼
User enters data
      │
      ▼
Create New Student
```

Update:

```text
Existing Student
      │
      ▼
Load Current Data
      │
      ▼
Show Pre-filled Form
      │
      ▼
User edits data
      │
      ▼
Update Existing Student
```

The biggest difference is that **Update begins by loading existing data**.

---

## How Does Django Know Which Student to Edit?

Exactly the same way our Detail page works.

Suppose the user clicks:

```text
Edit
```

for John.

The browser opens:

```text
/students/1/edit/
```

For Alice:

```text
/ students/2/edit/
```

For Bob:

```text
/students/3/edit/
```

The number in the URL tells Django which student should be edited.

---

## The Request Flow

The flow is almost identical to the Detail page.

```text
Browser
     │
     ▼
/students/2/edit/
     │
     ▼
urls.py
     │
     ▼
student_update()
     │
     ▼
get_object_or_404()
     │
     ▼
Database
     │
     ▼
Student Object
     │
     ▼
Template
     │
     ▼
Pre-filled Form
```

Notice something.

This is exactly what we learned in **Read (Detail)**.

The only difference is:

Instead of displaying:

```text
Name: Alice
```

we display:

```text
Name:
[Alice________]
```

The data is shown **inside form fields**.

---

## Why Don't We Start With Saving?

Many beginners think Update starts here:

```python
student.name = request.POST.get("name")
student.save()
```

But that's actually the **second half** of an update.

The **first half** is much more important:

1. Find the existing student.
2. Show the existing data.
3. Let the user edit it.

Only then can we save the changes.

That's why we're learning it in this order.

---

## Visual Comparison

### Create

```text
Database

(No student yet)
        │
        ▼
Blank Form
        │
User enters data
        │
        ▼
Create Student
```

#

### Update

```text
Database

John
        │
        ▼
Load John
        │
        ▼
Pre-filled Form
        │
User edits data
        │
        ▼
Update John
```

---

## Today's Goal

By the end of today's lesson, you should understand:

* ✅ An update modifies an existing record instead of creating a new one.
* ✅ The edit page starts with existing data already filled in.
* ✅ Django uses the student ID in the URL to determine which record to edit.
* ✅ The first step of every update operation is retrieving the existing object, not saving changes.

We haven't written any code yet because it's important to understand the workflow before implementing it.

---

## Next Lesson

Now that you understand the concept, we'll build the **Edit** page by creating a new URL and view:

```python
path(
    "students/<int:id>/edit/",
    views.student_update,
    name="student_update"
)
```

We'll retrieve the student with `get_object_or_404()`, just like we did for the Detail page, and display a form containing that student's current information. This will complete the **first half** of the Update operation before we learn how to save the changes.
