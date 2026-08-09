**Phase 2 – Models**

## Step 3: Understanding Django Field Types

In the previous lesson, we created this model:

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
```

You already know **how** to write it.

Now let's understand **why** we chose those field types.

---

## What is a Field Type?

A field type tells Django:

> **"What kind of data will be stored here?"**

Think of it as choosing the correct container for your data.

For example:

| Data            | Correct Container |
| --------------- | ----------------- |
| Name            | Text              |
| Age             | Number            |
| Email           | Email             |
| Birthday        | Date              |
| Active/Inactive | True or False     |

Django provides different field types for each kind of data.

---

## 1. CharField

```python
models.CharField(max_length=100)
```

### Purpose

Stores **short text**.

Examples:

```
Baloram Roy
```

```
Dhaka
```

```
Bangladesh
```

```
System Engineer
```

#

### Why "Char"?

It comes from **Character**.

A `CharField` stores a sequence of characters.

#

### Why `max_length`?

Every `CharField` must have a maximum size.

Example:

```python
name = models.CharField(max_length=100)
```

means

> This field can store **up to 100 characters**.

#

### Typical Uses

* Name
* Username
* City
* Country
* Job Title

---

## 2. TextField

```python
models.TextField()
```

### Purpose

Stores **large amounts of text**.

Imagine a blog application.

A blog post could contain hundreds or thousands of words.

Example:

```
Today I learned Django models...
```

A very long paragraph.

---

## Difference from CharField

### CharField

```
John Smith
```

Small text.

---

### TextField

```
Today I visited...
Many paragraphs...
Lots of information...
```

Large text.

#

### Real Examples

Good for:

* Article
* Description
* Biography
* Comments
* Notes

---

## Comparison

| CharField             | TextField                    |
| --------------------- | ---------------------------- |
| Short text            | Long text                    |
| Requires `max_length` | Doesn't require `max_length` |
| Name                  | Blog Content                 |

---

## 3. EmailField

```python
models.EmailField()
```

Purpose:

Store an email address.

Example:

```
abc@gmail.com
```

```
user@example.com
```

#

### Why not CharField?

Technically you *could* store an email using a `CharField`.

But Django provides `EmailField` because it understands the value is meant to be an email address.

Later, when we build forms, Django can automatically validate that the user entered something that looks like a valid email.

#

### Typical Uses

* Email
* Contact Email
* Login Email

---

## 4. IntegerField

```python
models.IntegerField()
```

Purpose:

Store whole numbers.

Examples:

```
10
```

```
20
```

```
100
```

---

Not valid:

```
Twenty
```

```
15.5
```

because an `IntegerField` only accepts integers.

#

### Typical Uses

* Age
* Quantity
* Stock
* Employee ID
* Marks

---

## 5. BooleanField

```python
models.BooleanField()
```

Purpose:

Store only two possible values.

```
True
```

or

```
False
```

Think of it as a simple **Yes/No** or **On/Off** switch.

#

### Real-Life Examples

Is the student active?

```
True
```

Has the payment been completed?

```
False
```

Is the account verified?

```
True
```

#

### Typical Uses

* Active User
* Published
* Verified
* Deleted (soft delete)
* Approved

---

## 6. DateField

```python
models.DateField()
```

Purpose:

Store a calendar date.

Example:

```
2026-08-05
```

#

### Typical Uses

* Birthday
* Joining Date
* Admission Date
* Hire Date

---

## Which Field Should You Choose?

Suppose you're building a Student Management System.

| Information   | Field Type     |
| ------------- | -------------- |
| Name          | `CharField`    |
| Email         | `EmailField`   |
| Age           | `IntegerField` |
| Address       | `TextField`    |
| Is Active     | `BooleanField` |
| Date of Birth | `DateField`    |

Notice how each piece of information naturally maps to a different field type.

---

## Revisiting Our Student Model

Our current model is:

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
```

This is a good choice because:

* `name` is short text → `CharField`
* `email` is an email address → `EmailField`
* `age` is a whole number → `IntegerField`

---

## Mental Model

Think of a model as a paper registration form.

```
Student Registration

Name: _______________________

Email: ______________________

Age: ________________________

Active: □ Yes   □ No

Date of Birth: _______________

Address:
_________________________________
_________________________________
```

Each box on the form expects a different type of information. Django field types tell the database exactly what each box is meant to contain.

---

## Phase 2 Summary

You now understand:

* ✅ What a Django Model is
* ✅ How to create a Model
* ✅ Why a Model inherits from `models.Model`
* ✅ What a Field is
* ✅ When to use:

  * `CharField`
  * `TextField`
  * `EmailField`
  * `IntegerField`
  * `BooleanField`
  * `DateField`

At this point, you've **only described** your data. Nothing has been created in the database yet.

---

## Next Phase

According to the roadmap, the next step is **Phase 3 – Migrations**. There we'll learn:

* What migrations are
* Why Django needs them
* What `makemigrations` does
* What `migrate` does
* How your `Student` model becomes an actual database table

Only after that will we inspect the database, exactly following the roadmap. 
