**Phase 2 – Models**

Today we'll **write our first model**, but we **will not** create a database table yet. We are only defining the blueprint.

---

# Step 2: Writing Your First Model

Open your app's `models.py`.

It currently looks something like this:

```python
from django.db import models

# Create your models here.
```

The first line:

```python
from django.db import models
```

imports Django's Model system.

Think of it like importing a toolbox.

Inside this toolbox are many field types such as:

* `CharField`
* `EmailField`
* `IntegerField`
* `DateField`
* `BooleanField`

We'll only use three of them today.

---

## Creating the Student Model

Below the import, write:

```python
from django.db import models


class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
```

Don't run anything yet.

Let's understand every line.

---

## Line 1

```python
class Student(models.Model):
```

This defines a new Python class named **Student**.

The part inside the parentheses:

```python
models.Model
```

means:

> "This class is a Django Model."

Without inheriting from `models.Model`, Django would treat it as an ordinary Python class and would not manage it as part of the database.

---

## Visual Representation

Think of it like this:

```text
Python Class
      │
      ▼
Student
      │
inherits from
      ▼
models.Model
      │
      ▼
Django knows this is a Model
```

---

## First Field

```python
name = models.CharField(max_length=100)
```

Here:

* `name` is the field name.
* `CharField` stores text.
* `max_length=100` means the field can hold up to 100 characters.

Examples of valid values:

```text
Alice

John Smith

Baloram Roy
```

---

## Why is `max_length` Required?

Imagine creating a database column without specifying how much text it can store.

Django needs to know the maximum size so it can create the correct database column later.

For example:

```python
max_length=20
```

allows:

```
John
```

but something much longer than 20 characters would not fit.

Today, just remember:

> `CharField` **requires** `max_length`.

We'll explore validation and database behavior in more detail later.

---

## Second Field

```python
email = models.EmailField()
```

This stores an email address.

Examples:

```text
abc@example.com

student@gmail.com
```

Notice we did **not** write:

```python
max_length=100
```

Even though `EmailField` is stored as text internally, Django provides a specialized field because it understands that the data represents an email address.

Later, when we build forms, Django can use this information to validate email input automatically.

---

## Third Field

```python
age = models.IntegerField()
```

This stores whole numbers.

Examples:

```text
18

20

25
```

Not allowed:

```text
Twenty

18.5
```

because an `IntegerField` accepts integers only.

---

## Putting It All Together

Our model now looks like this:

```python
from django.db import models


class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
```

Conceptually, this describes:

| Field | Data Type | Example                                       |
| ----- | --------- | --------------------------------------------- |
| name  | Text      | Alice                                         |
| email | Email     | [alice@example.com](mailto:alice@example.com) |
| age   | Integer   | 20                                            |

---

## What Has Happened So Far?

At this point:

✅ We have written a Python class.

✅ We have described our data structure.

❌ No database table exists yet.

❌ No data has been stored.

❌ No CRUD operations have been performed.

This is exactly what the roadmap intends for Phase 2. The actual database table will be created in **Phase 3 – Migrations**. 

---

## Mental Model

Think of your project like an architect designing a house.

```text
Architect draws blueprint
          │
          ▼
Construction starts later
```

Your `Student` model is the **blueprint**.

The database table is the **building**.

We have only finished the blueprint.

---

## Today's Learning Checklist

By the end of this lesson, you should understand:

* ✅ Why a model inherits from `models.Model`
* ✅ What `CharField` is used for
* ✅ Why `CharField` needs `max_length`
* ✅ What `EmailField` is used for
* ✅ What `IntegerField` is used for
* ✅ That writing a model **does not** create a database table

---

## Next Lesson (Still Phase 2)

Before moving to Phase 3 (Migrations), we'll spend one more lesson understanding **field types** in Django:

* `CharField`
* `TextField`
* `EmailField`
* `IntegerField`
* `BooleanField`
* `DateField`

We won't use all of them yet, but understanding when and why each one is used will make the model you just wrote much more meaningful. After that, we'll move to **Phase 3 – Migrations** exactly as the roadmap specifies.
