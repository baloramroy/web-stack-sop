### This is where Django becomes **dynamic**.
- Until now, every page was **static**:
  ```html
  <h2>Home Page</h2>

  <p>Welcome to my Django website.</p>
  ```

- No matter **who visits** the page, everyone sees **exactly the same content.**
- Now we're going to learn how a **view sends data to a template**.
- This concept is called **Context**.

---

# Lesson 5: Passing Data from a View to a Template (Context)

## Learning Objectives

By the end of this lesson, you will understand:

1. What a context is.
2. Why we use a context.
3. How a view sends data to a template.
4. How a template displays that data.
5. The relationship between Python variables and template variables.

---

## Why Do We Need Context?

- **Suppose you have this template:**

  ```html
  <h2>Home Page</h2>

  <p>Welcome to my Django website.</p>
  ```

  > This text is hardcoded.

- **What if you want:**

  ```
  Welcome Baloram
  ```

  **or**

  ```
  Welcome Alice
  ```

  **or**

  ```
  Welcome John
  ```

  >◼️ The template alone cannot decide that.\
  >◼️The **view** must provide the data.

- **Think of it like this:**

  ```
  View
      │
      │ sends data
      ▼
  Template
      │
      ▼
  Browser
  ```

---

## Real-Life Analogy

◼️ Imagine you're filling out a certificate.

- **The certificate design never changes.**

  ```
  Certificate

  This certifies that

  _____________

  has completed the course.
  ```

- **Only the student's name changes.**

  ```
  Baloram

  Alice

  John

  Rahim
  ```

- The blank space is filled with data.
- The certificate is the **template**.
- The student's name is the **context**.

---

## What is Context?

◼️ A context is simply a **Python dictionary**.

- **Example:**

  ```python
  {
      "name": "Baloram",
      "course": "Django",
  }
  ```

  > Nothing special.

**It's just a dictionary.**

- Keys:

  ```
  name
  course
  ```

- Values:

  ```
  Baloram
  Django
  ```

---

## Step 1: Update `views.py`

- **Let's modify the `home` view.**

  ```python
  from django.shortcuts import render

  def home(request):
      context = {
          "name": "Baloram",
          "course": "Django",
      }

      return render(request, "home.html", context)
  ```

  > Notice something new.

- **Before:**

  ```python
  return render(request, "home.html")
  ```

- **Now:**

  ```python
  return render(request, "home.html", context)
  ```

  > We added a third argument.

#

### Understanding `render()`

- **The `render()` function looks like this:**

  ```python
  render(request, template_name, context)
  ```

◼️ Let's understand each argument.

- **First Argument**

  ```python
  request
  ```

  > The user's HTTP request.


- **Second Argument**

  ```python
  "home.html"
  ```

  > The template to render.


- **Third Argument**

  ```python
  context
  ```

  > The data you want to send to the template.


- **Think of it like this:**

  ```
  render(
      request,
      template,
      data
  )
  ```

---

## Step 2: Update `home.html`

- Replace the content block with:

  ```django
  {% extends "base.html" %}

  {% block content %}

  <h2>Home Page</h2>

  <p>Welcome {{ name }}</p>

  <p>Course: {{ course }}</p>

  {% endblock %}
  ```

#

### What is `{{ }}`?

◼️ This is called **variable interpolation** in the Django Template Language (DTL).

**It means:**

> "Display the value of this variable."

- Example:

  ```
  {{ name }}
  ```

**Django asks:**

> Is there a variable called `name` in the context?

- Yes.

  ```
  "name": "Baloram"
  ```

- So it prints:

  ```
  Baloram
  ```

#

### What Happens Behind the Scenes?

- **View:**

  ```python
  context = {
      "name": "Baloram",
  }
  ```

  ↓

- **Template:**

  ```django
  {{ name }}
  ```

  ↓

- **Browser:**

  ```html
  Baloram
  ```

#

◼️ Another example:

- **View:**

  ```python
  context = {
      "course": "Django",
  }
  ```

  ↓

- **Template:**

  ```django
  {{ course }}
  ```

  ↓

- **Browser:**

  ```html
  Django
  ```

---

## Complete Request Flow

- Example:
  
  ```
  Browser

  ↓

  Request

  ↓

  home()

  ↓

  context = {
      "name": "Baloram",
      "course": "Django"
  }

  ↓

  render()

  ↓

  home.html

  ↓

  {{ name }}
  ↓

  Baloram

  ↓

  {{ course }}
  ↓

  Django

  ↓

  HTML

  ↓

  Browser
  ```

---

## Understanding the Dictionary

- Suppose:

  ```python
  context = {
      "city": "Dhaka",
  }
  ```

- Then:

  ```django
  {{ city }}
  ```

- prints:

  ```
  Dhaka
  ```

#

- Suppose:

  ```python
  context = {
      "company": "OpenAI",
  }
  ```

- Then:

  ```django
  {{ company }}
  ```

- prints:

  ```
  OpenAI
  ```

#

- The rule is very simple:

  ```
  Dictionary Key

  ↓

  Template Variable

  ↓

  Displayed Value
  ```

---

## Important Rule

◼️ The **key** in the context dictionary must match the **template variable**.

◼️ **Example:**

- **View:**

  ```python
  context = {
      "username": "Baloram",
  }
  ```

- **Template:**

  ```django
  {{ username }}
  ```

  > ✅ Works.

#

◼️ **But this:**

- **View:**

  ```python
  context = {
      "username": "Baloram",
  }
  ```

- **Template:**

  ```django
  {{ name }}
  ```

  > ❌ Doesn't work.

Because there is no key named `name`.

---

## Can We Pass Numbers?

◼️ `Yes` we can pass the number

- **View:**

  ```python
  context = {
      "age": 25,
  }
  ```

- **Template:**

  ```django
  {{ age }}
  ```

- **Output:**

  ```
  25
  ```

---

## Can We Pass Booleans?

◼️ Yes we can pass the booleans.

- **View:**
- 
  ```python
  context = {
      "is_admin": True,
  }
  ```

- Template:

  ```django
  {{ is_admin }}
  ```

- Output:

  ```
  True
  ```

  > Later we'll use this with `{% if %}`.

---

## Can We Pass Multiple Values?

- **Absolutely.**

  ```python
  context = {
      "name": "Baloram",
      "age": 25,
      "city": "Dhaka",
      "course": "Django",
  }
  ```

- **Template:**

  ```django
  Name: {{ name }}

  Age: {{ age }}

  City: {{ city }}

  Course: {{ course }}
  ```

- **Output:**

  ```
  Name: Baloram

  Age: 25

  City: Dhaka

  Course: Django
  ```

---

## A Small Challenge

- **Try changing your `home` view to:**

  ```python
  def home(request):
      context = {
          "student_name": "Baloram Roy",
          "profession": "IT Support Engineer",
          "country": "Bangladesh",
          "course": "Learning Django",
      }

      return render(request, "home.html", context)
  ```

- **Then update `home.html`:**

  ```django
  {% extends "base.html" %}

  {% block content %}

  <h2>Student Information</h2>

  <p>Name: {{ student_name }}</p>
  <p>Profession: {{ profession }}</p>
  <p>Country: {{ country }}</p>
  <p>Course: {{ course }}</p>

  {% endblock %}
  ```

When you refresh the page, all four values should appear.

---

## Summary

| Component                               | Purpose                                                      |
| --------------------------------------- | ------------------------------------------------------------ |
| `context`                               | A Python dictionary containing data to send to the template. |
| `render(request, "home.html", context)` | Renders the template and makes the context available to it.  |
| `{{ variable }}`                        | Displays the value of a context variable in the template.    |

---

## Homework

Before moving to the next lesson, make sure you can answer these questions:

1. What is a context in Django?
2. Why is a context a dictionary?
3. What are the three arguments passed to `render()`?
4. Why must the dictionary key match the template variable name?
5. What will happen if the template uses `{{ email }}` but the context doesn't contain an `email` key?

---

## Next Lesson

The next lesson will cover the other major part of the Django Template Language:

* `{% if %}` — show content conditionally.
* `{% for %}` — display lists of data.
* Accessing dictionary values and object attributes.

These features let your templates make decisions and display collections of data, which is essential before we move on to models and databases.

---