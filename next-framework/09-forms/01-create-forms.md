**Phase 8 — Forms**

# Step 1 — Create Forms

Today we're **not submitting data yet**. That is Step 2.

Today's goal is only to understand **what a Django Form is** and create one.

---

## What is a Form?

Think about a website like Facebook.

When you register, you see boxes like:

```
Name
Email
Password
Confirm Password

[ Register ]
```

Those boxes together are called a **form**.

A form is simply a way to collect information from the user.

Examples:

* Login
* Registration
* Contact Us
* Search Box
* Change Password
* Edit Profile
* Feedback Form

All of these are forms.

---

## Without Django Forms

Imagine asking someone their name.

Without Django Forms:

```
User types name

↓

You manually check

- Is it empty?
- Is it too long?
- Is it valid?
- Is it required?
```

You write all the checking yourself.

Lots of code.

---

## With Django Forms

Django says:

> "Tell me what fields you need.
> I'll help create the HTML and validate the data."

Much easier.

---

## Django Form Flow

```
Browser

↓

HTML Form

↓

forms.py

↓

View

↓

Database (optional)
```

Notice something important.

Today's lesson stops here:

```
Browser

↓

HTML

↓

forms.py
```

We are **not saving anything yet**.

---

## What is forms.py?

Just like Django has

```
models.py
```

for database models,

it also usually has

```
forms.py
```

for forms.

Example project:

```
myapp/

    models.py

    views.py

    urls.py

    forms.py

    admin.py
```

If it doesn't exist, you simply create it.

---

## Create forms.py

Inside your app:

```
myapp/

    forms.py
```

---

## Your First Form

Open

```
forms.py
```

Write:

```python
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)
```

Don't worry about every line yet. Let's understand them one by one.

#

### Line 1

```python
from django import forms
```

This imports Django's form library.

Just like:

```python
from django.db import models
```

imports database models.

#

### Line 2

```python
class ContactForm(forms.Form):
```

You are creating a new form named:

```
ContactForm
```

It inherits from:

```
forms.Form
```

meaning "this is a Django form."

#

### Field 1

```python
name = forms.CharField(max_length=100)
```

Creates a text input.

Rendered in HTML as something like:

```
+----------------------+
| John                 |
+----------------------+
```

#

### Field 2

```python
email = forms.EmailField()
```

Creates an email field.

Django knows it should contain a valid email address.

Example:

```
abc@example.com
```

#

### Field 3

```python
message = forms.CharField(
    widget=forms.Textarea
)
```

Instead of a single-line input, this creates a multi-line text box.

Like:

```
+----------------------+
| Hello...             |
|                      |
|                      |
+----------------------+
```

Perfect for messages or comments.

---

## What Django Creates

From only:

```python
name = forms.CharField()
```

Django knows:

* It is required (by default)
* It is a text field
* It should be validated
* It can show errors if invalid

That's one of the biggest benefits of Django Forms.

---

## Form vs Model

This is a common point of confusion.

| Model                         | Form                        |
| ----------------------------- | --------------------------- |
| Stores data in the database   | Collects data from the user |
| Defined in `models.py`        | Defined in `forms.py`       |
| Represents database structure | Represents user input       |

Think of it this way:

* **Model** = "How data is stored."
* **Form** = "How data is entered."

---

## What We Learned Today

✅ What a form is

✅ Why Django Forms are useful

✅ The purpose of `forms.py`

✅ How to create your first form

✅ Basic field types:

* `CharField`
* `EmailField`
* `Textarea`

---

## Practice

1. Create a new file named `forms.py` in your Django app (if it doesn't already exist).
2. Add the `ContactForm` class exactly as shown above.
3. Read through each field and make sure you understand what it represents.

**Don't connect it to a view or template yet.** We'll do that in **Step 2 — Handle Form Submission**, where you'll learn how a form is displayed, how data is submitted, and how Django processes it.
