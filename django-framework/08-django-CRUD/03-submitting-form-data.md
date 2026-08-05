**Phase 5 — CRUD: Create Operation**

# Lesson: Submitting Form Data (HTTP POST)

In the previous lesson, we built the page that displays the form.

Today, we'll make the **Save** button actually send the data to the Django view.

> **Important:** We are still not saving to the database in this lesson. We will first learn how data travels from the browser to the view.

---


## Goal

When the user fills in the form:

```text
Name : John
Email: john@example.com
Age  : 22
```

and clicks **Save**, the browser should send that data to Django.

The flow becomes:

```text
Browser
     │
User fills form
     │
Clicks Save
     │
     ▼
POST Request
     │
     ▼
student_create()
     │
     ▼
Read submitted data
```

Notice that the database is still **not involved**.

---

## Step 1 — Update the Form

Open:

```text
templates/myapp/student_form.html
```

Change the `<form>` tag to:

```html
<form method="POST">
    {% csrf_token %}
```

Your form now starts like this:

```html
<form method="POST">
    {% csrf_token %}

    <p>
        <label>Name</label><br>
        <input type="text" name="name">
    </p>

    <p>
        <label>Email</label><br>
        <input type="email" name="email">
    </p>

    <p>
        <label>Age</label><br>
        <input type="number" name="age">
    </p>

    <button type="submit">
        Save
    </button>

</form>
```

---

## Why `method="POST"`?

HTML forms can send data in different ways.

The two you'll use most often are:

| Method | Purpose                 |
| ------ | ----------------------- |
| GET    | Retrieve data           |
| POST   | Send data to the server |

Since we're sending new student information, we use:

```html
method="POST"
```

---

## Why `{% csrf_token %}`?

Django protects forms against **Cross-Site Request Forgery (CSRF)** attacks.

Every POST form should include:

```django
{% csrf_token %}
```

If you forget it, Django will usually return:

```text
403 Forbidden

CSRF verification failed.
```

So, whenever you create an HTML form that submits with `POST`, make it a habit to include the CSRF token.

---

## Step 2 — Detect a POST Request

Open `views.py`:

```python
from django.shortcuts import render

def student_create(request):

    if request.method == "POST":
        print("Form Submitted!")

    return render(request, "myapp/student_form.html")
```

---

## Understanding `request.method`

Every request has a method.

If the user simply visits:

```text
/students/add/
```

then:

```python
request.method
```

is:

```text
GET
```

If the user clicks **Save**, then:

```python
request.method
```

becomes:

```text
POST
```

So this code:

```python
if request.method == "POST":
```

asks:

> "Did the user submit the form?"

If the answer is yes, the code inside the `if` block runs.

---

## Step 3 — Read the Submitted Data

Replace your view with:

```python
from django.shortcuts import render

def student_create(request):

    if request.method == "POST":

        name = request.POST.get("name")
        email = request.POST.get("email")
        age = request.POST.get("age")

        print(name)
        print(email)
        print(age)

    return render(request, "myapp/student_form.html")
```

---

## Understanding `request.POST`

When the browser submits the form, Django stores the submitted values in:

```python
request.POST
```

Think of it like a dictionary.

If the user entered:

```text
Name : John
Email: john@example.com
Age  : 22
```

then:

```python
request.POST
```

contains something similar to:

```python
{
    "name": "John",
    "email": "john@example.com",
    "age": "22"
}
```

You can retrieve each value using:

```python
request.POST.get("name")
```

or:

```python
request.POST.get("email")
```

or:

```python
request.POST.get("age")
```

---

## Step 4 — Test It

Run your server:

```bash
python manage.py runserver
```

Open:

```text
http://127.0.0.1:8000/students/add/
```

Fill in:

```text
Name : John
Email: john@example.com
Age  : 22
```

Click **Save**.

Look at the terminal where `runserver` is running.

You should see something like:

```text
John
john@example.com
22
```

This proves that:

* The browser submitted the form.
* Django received the POST request.
* The view accessed the submitted values.

---

## What We've Learned

Today's flow is:

```text
Browser
      │
      ▼
Student Form
      │
      ▼
POST Request
      │
      ▼
request.method == "POST"
      │
      ▼
request.POST
      │
      ▼
Read submitted values
```

Still **not happening**:

* ❌ No `Student` object created.
* ❌ No database insert.
* ❌ No validation.
* ❌ No redirect after submission.

Those are separate responsibilities, and we'll add them one by one.

---

## Next Lesson

In the next step, we'll take the submitted values and create the first `Student` object using the Django model, completing your first **Create** operation by saving a record to the database.
