**Phase 5 → CRUD → Read (Detail)**

Excellent. We have now completed:

* ✅ Create
* ✅ Read (List)

According to the roadmap, the next CRUD topic is:

> **Read (Detail)** 

As always, we'll go **one small step at a time**.

# Lesson 1: What is a Detail Page?

Before writing any code, let's understand the concept.

So far, our application displays **all students**.

Example:

| ID | Name  | Email                                         | Age |
| -- | ----- | --------------------------------------------- | --- |
| 1  | John  | [john@example.com](mailto:john@example.com)   | 22  |
| 2  | Alice | [alice@example.com](mailto:alice@example.com) | 21  |
| 3  | Bob   | [bob@example.com](mailto:bob@example.com)     | 24  |

This is called a **List View** because it lists multiple records.

---

## The Problem

Suppose you want to see **all information about Alice**.

Should you keep displaying every student?

No.

Instead, you open a page dedicated to Alice.

For example:

```text
/students/2/
```

Now the page displays only:

```text
Student Details

ID: 2

Name: Alice

Email: alice@example.com

Age: 21
```

This is called a **Detail View**.

---

## List vs Detail

### List

URL:

```text
/students/
```

Result:

```text
John

Alice

Bob
```

Many records.

#

### Detail

URL:

```text
/students/2/
```

Result:

```text
Alice

alice@example.com

21
```

One record.

---

## How Does Django Know Which Student?

This is the most important concept in today's lesson.

Look at the URL:

```text
/students/2/
```

What does the **2** mean?

It is the **ID** of the student.

Database:

| ID | Name  |
| -- | ----- |
| 1  | John  |
| 2  | Alice |
| 3  | Bob   |

When Django receives:

```text
/students/2/
```

it understands:

> "Find the student whose ID is 2."

Likewise:

```text
/students/1/
```

means:

> "Find John."

And:

```text
/students/3/
```

means:

> "Find Bob."

---

## The Request Flow

The request flow is very similar to what you've already learned.

```text
Browser
    │
    ▼
/students/2/
    │
    ▼
urls.py
    │
    ▼
student_detail()
    │
    ▼
Student.objects.get(id=2)
    │
    ▼
Database
    │
    ▼
One Student Object
    │
    ▼
Template
    │
    ▼
Browser
```

Notice the difference from the List page.

#

### Read (List)

```python
Student.objects.all()
```

returns:

```text
Many students
```

#

### Read (Detail)

```python
Student.objects.get(...)
```

returns:

```text
One student
```

This is the key difference.

---

## Visual Comparison

### Read (List)

```text
Database

John

Alice

Bob
```

↓

```python
Student.objects.all()
```

↓

```text
QuerySet

John

Alice

Bob
```

#

### Read (Detail)

```text
Database

John

Alice

Bob
```

↓

```python
Student.objects.get(id=2)
```

↓

```text
Alice
```

Only one object is returned.

---

## Why Not Use `all()`?

Suppose the URL is:

```text
/students/2/
```

If we wrote:

```python
students = Student.objects.all()
```

Django would still retrieve:

* John
* Alice
* Bob

But we only need Alice.

That would be unnecessary work.

Instead, we ask Django for **one specific object**.

---

## What Will We Build?

By the end of this topic, you'll be able to visit:

```text
/students/1/
```

and see:

```text
Student Details

ID: 1

Name: John

Email: john@example.com

Age: 22
```

If you visit:

```text
/students/3/
```

you'll see Bob's information instead.

The same page works for every student because the **ID in the URL changes**.

---

## Today's Goal

By the end of today's lesson, you should understand:

* ✅ The difference between **Read (List)** and **Read (Detail)**.
* ✅ Why a detail page displays only one record.
* ✅ How the student ID in the URL identifies which record to retrieve.
* ✅ Why `Student.objects.get(...)` is used instead of `Student.objects.all()`.

Notice that we **haven't written any new code yet**. Just as we did with Create and Read (List), we first build the mental model.

---

## Next Lesson

Now that you understand the concept, we'll start implementing it by learning **URL parameters**. You'll create a route like:

```python
path(
    "students/<int:id>/",
    views.student_detail,
    name="student_detail"
)
```

and learn how Django captures the `id` from the URL and passes it into your view. This is the foundation of every Django detail page.
