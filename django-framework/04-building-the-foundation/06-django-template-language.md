# Lesson 6: Django Template Language (DTL)

So far you've learned:

* ✅ Project & App structure
* ✅ URL routing
* ✅ Views
* ✅ Templates
* ✅ Template inheritance
* ✅ Passing data (Context)

Now we're going to make templates **intelligent**.

---

## Learning Objectives

By the end of this lesson, you will understand:

1. `{{ variable }}` (Review)
2. `{% if %}`
3. `{% else %}`
4. `{% elif %}`
5. `{% for %}`
6. Accessing dictionary values
7. Accessing object attributes
8. The difference between `{{ }}` and `{% %}`

---

## First, Let's Understand DTL

- DTL stands for **Django Template Language**.

- It allows you to add **logic** to your HTML.

Without DTL:

```html
<h1>Welcome</h1>
```

With DTL:

```django
<h1>Welcome {{ name }}</h1>
```

or

```django
{% if is_logged_in %}
    <h1>Welcome</h1>
{% endif %}
```

>Notice something? \
> There are **two different syntaxes**.

---

## Rule #1

### `{{ }}` → Display Data

Example:

```django
{{ name }}
```

This means:

> Show the value.

Think:

```text
Display something
```

Examples:

```django
{{ name }}

{{ age }}

{{ city }}

{{ email }}
```

> These all print values.

---

## Rule #2

### `{% %}` → Perform Logic

Examples:

```django
{% if %}
```

```django
{% for %}
```

```django
{% extends %}
```

```django
{% block %}
```

- These **do not display data**.

- They tell Django to **do something**.

Think:

```text
Action

Decision

Loop

Control
```

---

## Easy Way to Remember

| Syntax  | Purpose                |
| ------- | ---------------------- |
| `{{ }}` | Show a value           |
| `{% %}` | Execute template logic |

> This is one of the most important rules in Django.

---

## Part 1 — `{% if %}`

**Suppose your view is:**

```python
def home(request):

    context = {
        "is_logged_in": True
    }

    return render(request, "home.html", context)
```

**Now inside the template:**

```django
{% if is_logged_in %}

<h2>Welcome Back!</h2>

{% endif %}
```

**What happens?**

`is_logged_in` is `True`.

**So Django displays:**

```html
<h2>Welcome Back!</h2>
```

**Now change it.**

```python
"is_logged_in": False
```

- Refresh.
- Nothing appears.
- Because the condition failed.

#

### Think of it like Python.

Python:

```python
if is_logged_in:
    print("Welcome")
```

DTL:

```django
{% if is_logged_in %}

Welcome

{% endif %}
```

> Very similar.

#

### `{% else %}`

View:

```python
context = {
    "is_logged_in": False
}
```

Template:

```django
{% if is_logged_in %}

<h2>Welcome</h2>

{% else %}

<h2>Please Login</h2>

{% endif %}
```

Output:

```html
Please Login
```

**Now make it True.**

Output becomes

```html
Welcome
```

---

### `{% elif %}`

Suppose

```python
context = {
    "marks": 80
}
```

Template:

```django
{% if marks >= 80 %}

Grade A

{% elif marks >= 60 %}

Grade B

{% else %}

Fail

{% endif %}
```

Output:

```
Grade A
```

> Notice how similar it is to Python.

---

## Part 2 — `{% for %}`

◼️ **NOTE:** This is probably the most used template tag after `if`.

**Suppose the view sends:**

```python
context = {
    "courses": [
        "Python",
        "Linux",
        "Django",
        "Docker"
    ]
}
```

**The template:**

```django
{% for course in courses %}

<p>{{ course }}</p>

{% endfor %}
```

**Output:**

```html
Python

Linux

Django

Docker
```

#

**Think of it exactly like Python.**

Python:

```python
for course in courses:
    print(course)
```

Template:

```django
{% for course in courses %}

{{ course }}

{% endfor %}
```

#

**Example with HTML**

```django
<ul>

{% for course in courses %}

<li>{{ course }}</li>

{% endfor %}

</ul>
```

Output

```html
<ul>

<li>Python</li>

<li>Linux</li>

<li>Django</li>

<li>Docker</li>

</ul>
```

> Now your page becomes dynamic.

---

## Part 3 — Accessing Dictionary Values

**View:**

```python
context = {
    "student": {
        "name": "Baloram",
        "city": "Dhaka",
        "age": 25
    }
}
```

**Many beginners think they should write:**

```django
{{ student["name"] }}
```

- ❌ Wrong.

- In Django templates you use **dot notation**.

**Correct:**

```django
{{ student.name }}

{{ student.city }}

{{ student.age }}
```

**Output**

```text
Baloram

Dhaka

25
```

#

### Why Dot Notation?

Python:

```python
student["name"]
```

Django Template:

```django
student.name
```

>Django keeps the template language simple by hiding Python syntax.

---

## Part 4 — Accessing Object Attributes

Later we'll have models.

**Imagine:**

```python
student.name

student.email

student.age
```

**Templates are exactly the same.**

```django
{{ student.name }}

{{ student.email }}

{{ student.age }}
```

> That's why learning dot notation now is important.

**It works for both:**

* Dictionaries
* Model objects

---

## Complete Example

### views.py

```python
from django.shortcuts import render

def home(request):

    context = {
        "student": {
            "name": "Baloram Roy",
            "profession": "IT Support Engineer",
            "country": "Bangladesh"
        },

        "courses": [
            "Python",
            "Linux",
            "Django",
            "Docker"
        ],

        "is_logged_in": True
    }

    return render(request, "home.html", context)
```

#

### home.html

```django
{% extends "base.html" %}

{% block content %}

<h2>Student Information</h2>

<p>Name: {{ student.name }}</p>
<p>Profession: {{ student.profession }}</p>
<p>Country: {{ student.country }}</p>

<hr>

{% if is_logged_in %}
    <p>Welcome back!</p>
{% else %}
    <p>Please log in.</p>
{% endif %}

<hr>

<h3>Courses</h3>

<ul>
{% for course in courses %}
    <li>{{ course }}</li>
{% endfor %}
</ul>

{% endblock %}
```

---

## Request Flow (Now)

```text
Browser
        │
        ▼
Request
        │
        ▼
View
        │
        ▼
Context
        │
        ├── student
        ├── courses
        └── is_logged_in
        │
        ▼
Template
        │
        ├── {{ }}
        ├── {% if %}
        └── {% for %}
        │
        ▼
HTML
        │
        ▼
Browser
```

---

## Important Limitation

◼️ Templates are **not** meant for complex programming.

**Good:**

```django
{{ student.name }}
```

**Good:**

```django
{% if is_logged_in %}
```

**Good:**

```django
{% for course in courses %}
```

**Bad:**

```django
{{ student.calculate_salary() }}
```

**Bad:**

```django
{{ my_python_function() }}
```

**Why?**

Django follows the **separation of concerns** principle:

* **View** → Handles business logic and prepares data.
* **Template** → Displays data.

Keep your templates simple.

---

## Summary

| Syntax           | Purpose                                     | Example                       |
| ---------------- | ------------------------------------------- | ----------------------------- |
| `{{ variable }}` | Display a value                             | `{{ student.name }}`          |
| `{% if %}`       | Conditional display                         | `{% if is_logged_in %}`       |
| `{% else %}`     | Alternative branch                          | `{% else %}`                  |
| `{% elif %}`     | Multiple conditions                         | `{% elif marks >= 60 %}`      |
| `{% for %}`      | Loop through a collection                   | `{% for course in courses %}` |
| `student.name`   | Access dictionary keys or object attributes | `{{ student.name }}`          |

---

## Mini Practice (Highly Recommended)

◼️ Before we move to **Models**, try this on your own:

**Update your `home` view to send this context:**

```python
context = {
    "employee": {
        "name": "Baloram Roy",
        "department": "IT",
        "designation": "IT Support Engineer"
    },
    "skills": [
        "Linux",
        "Python",
        "Django",
        "Docker",
        "Ansible"
    ],
    "is_manager": False
}
```

**Then create a template that:**

1. Displays the employee's name, department, and designation.
2. Uses an `{% if %}` statement to display:

   * "Manager Access" if `is_manager` is `True`.
   * "Employee Access" if `is_manager` is `False`.
3. Uses a `{% for %}` loop to display all the skills in an unordered list.

---

## Next Lesson: Models (Your First Database Table)

You've now learned the core pieces of the presentation layer:

* ✅ URLs
* ✅ Views
* ✅ Templates
* ✅ Template inheritance
* ✅ Context
* ✅ Django Template Language

The next lesson is where we'll start working with data by learning **`models.py`**. We'll begin by creating a single model, understanding what a model represents, and seeing how it relates to a database table—without rushing into CRUD. This foundation will make the database side of Django much easier to understand.

---