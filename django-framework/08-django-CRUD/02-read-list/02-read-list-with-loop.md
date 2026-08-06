**Phase 5 → CRUD**
# Topic: Read (List) with loop

Last lesson, we learned:

```python
students = Student.objects.all()
```

We passed the QuerySet to the template:

```python
return render(
    request,
    "myapp/student_list.html",
    {
        "students": students
    }
)
```

Today we'll learn how to **display every student** using Django's template language.

---

## Today's Goal

Instead of seeing:

```text
<QuerySet [
    <Student: John>,
    <Student: Alice>,
    <Student: Bob>
]>
```

we want to display:

| ID | Name  | Email                                         | Age |
| -- | ----- | --------------------------------------------- | --- |
| 1  | John  | [john@example.com](mailto:john@example.com)   | 22  |
| 2  | Alice | [alice@example.com](mailto:alice@example.com) | 21  |
| 3  | Bob   | [bob@example.com](mailto:bob@example.com)     | 24  |

---

## How Can We Display Multiple Students?

Let's suppose your database contains three records.

When Django executes:

```python
students = Student.objects.all()
```

Think of the result like this:

```text
students
│
├── Student 1
├── Student 2
└── Student 3
```

The template needs a way to visit each student one by one.

That's exactly what the `{% for %}` tag does.

---

## Step 1 — Understanding `{% for %}`

The syntax is:

```django
{% for item in items %}

{% endfor %}
```

This means:

> "Take every object inside `items`, one at a time."

---

For our project:

```django
{% for student in students %}

{% endfor %}
```

Read it like English:

> "For every student inside students..."

Notice the naming:

```django
students
```

is the **entire collection**.

```django
student
```

is **one object** from that collection.

Think of it like this:

```text
students
    │
    ├── John
    ├── Alice
    └── Bob
```

During each loop:

First iteration:

```text
student = John
```

Second iteration:

```text
student = Alice
```

Third iteration:

```text
student = Bob
```

The loop repeats until every student has been processed.

---

## Step 2 — Display One Field

Open:

```text
templates/myapp/student_list.html
```

Replace the previous content with:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Student List</title>
</head>
<body>

<h1>Student List</h1>

{% for student in students %}

    <p>{{ student.name }}</p>

{% endfor %}

</body>
</html>
```

---

## Understanding `{{ student.name }}`

Remember Phase 1?

You learned:

```django
{{ name }}
```

to display a simple variable.

Now `student` is not a simple string.

It is a **Student model object**.

That object has fields:

```python
name
email
age
```

So:

```django
{{ student.name }}
```

means:

> "Display the value of the student's `name` field."

If your database contains:

| Name  |
| ----- |
| John  |
| Alice |
| Bob   |

The page becomes:

```text
Student List

John

Alice

Bob
```

---

## Step 3 — Display Multiple Fields

Now update the loop:

```html
{% for student in students %}

<p>
    {{ student.name }}
    -
    {{ student.email }}
    -
    {{ student.age }}
</p>

{% endfor %}
```

Now the browser displays:

```text
John - john@example.com - 22

Alice - alice@example.com - 21

Bob - bob@example.com - 24
```

Notice that we're still not using a table.

We're focusing only on understanding the loop.

---

## Step 4 — Convert It into an HTML Table

Now that you understand the loop, we can display the data more cleanly.

Replace the body with:

```html
<h1>Student List</h1>

<table border="1">

    <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Email</th>
        <th>Age</th>
    </tr>

    {% for student in students %}

    <tr>

        <td>{{ student.id }}</td>
        <td>{{ student.name }}</td>
        <td>{{ student.email }}</td>
        <td>{{ student.age }}</td>

    </tr>

    {% endfor %}

</table>
```

---

## What Happens During the Loop?

Suppose the database contains:

| ID | Name  | Email                                         | Age |
| -- | ----- | --------------------------------------------- | --- |
| 1  | John  | [john@example.com](mailto:john@example.com)   | 22  |
| 2  | Alice | [alice@example.com](mailto:alice@example.com) | 21  |
| 3  | Bob   | [bob@example.com](mailto:bob@example.com)     | 24  |

### First iteration

```text
student.id      = 1
student.name    = John
student.email   = john@example.com
student.age     = 22
```

Django generates:

```html
<tr>
    <td>1</td>
    <td>John</td>
    <td>john@example.com</td>
    <td>22</td>
</tr>
```

#

### Second iteration

```text
student.id      = 2
student.name    = Alice
student.email   = alice@example.com
student.age     = 21
```

Django generates:

```html
<tr>
    <td>2</td>
    <td>Alice</td>
    <td>alice@example.com</td>
    <td>21</td>
</tr>
```

#

### Third iteration

```text
student.id      = 3
student.name    = Bob
student.email   = bob@example.com
student.age     = 24
```

Django generates:

```html
<tr>
    <td>3</td>
    <td>Bob</td>
    <td>bob@example.com</td>
    <td>24</td>
</tr>
```

When the loop finishes, the browser displays one complete table with all the rows.

---

## The Complete Flow

```text
Database
    │
    ▼
Student.objects.all()
    │
    ▼
QuerySet
    │
    ▼
Context
    │
students
    │
    ▼
Template
    │
{% for student in students %}
    │
    ▼
One HTML row for each student
    │
    ▼
Browser
```

This is the standard pattern you'll use throughout Django whenever you need to display multiple records.

---

## What We Learned Today

Today you learned three fundamental template concepts:

* ✅ How a `QuerySet` is passed from the view to the template.
* ✅ How `{% for student in students %}` loops through every model object.
* ✅ How `{{ student.field_name }}` accesses individual model fields like `name`, `email`, `age`, and `id`.

With these concepts, you can display not only students but any collection of model objects in Django.

---

## Next Lesson

We'll improve the page by handling the situation where the database is empty. You'll learn Django's template `{% empty %}` clause, so instead of showing a blank table, your application will display a friendly message such as **"No students found."** This is a common pattern used in production Django applications.
