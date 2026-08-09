**Phase 5 → CRUD → Read (Detail)**
# Lesson: Dynamic Id Generation

The detail page works now, but there is one problem.

How does the user get to it?

Right now, the user has to manually type:

```text
/students/1/

/students/2/

/students/3/
```

That isn't a good user experience.

Today we'll connect the **Student List** page with the **Student Detail** page.

---

## Today's Goal

Current Student List:

| ID | Name  | Email                                         | Age |
| -- | ----- | --------------------------------------------- | --- |
| 1  | John  | [john@example.com](mailto:john@example.com)   | 22  |
| 2  | Alice | [alice@example.com](mailto:alice@example.com) | 21  |

After today's lesson:

| ID | Name  | Email                                         | Age | Action       |
| -- | ----- | --------------------------------------------- | --- | ------------ |
| 1  | John  | [john@example.com](mailto:john@example.com)   | 22  | View Details |
| 2  | Alice | [alice@example.com](mailto:alice@example.com) | 21  | View Details |

When the user clicks **View Details**, they should be taken to:

```text
/students/1/
```

or

```text
/students/2/
```

depending on which student they clicked.

---

## Hardcoded URLs vs Django URLs

Imagine writing this:

```html
<a href="/students/1/">
    View Details
</a>
```

This works...

...but only for student **1**.

For student **2**, you'd need:

```html
<a href="/students/2/">
```

For student **3**:

```html
<a href="/students/3/">
```

That isn't practical.

---

## Django's Solution

Django provides the **`url` template tag**.

Instead of writing the URL directly, we tell Django:

> "Generate the URL whose name is `student_detail`."

General syntax:

```django
{% url 'url_name' %}
```

If the URL needs parameters:

```django
{% url 'url_name' parameter %}
```

---

## Step 1 — Review `urls.py`

Our URL already exists:

```python
path(
    "students/<int:id>/",
    views.student_detail,
    name="student_detail"
)
```

Notice the important part:

```python
name="student_detail"
```

This name is what `{% url %}` uses.

---

## Step 2 — Update the List Template

Open:

```text
templates/myapp/student_list.html
```

Add another column.

```html
<table border="1">

<tr>
    <th>ID</th>
    <th>Name</th>
    <th>Email</th>
    <th>Age</th>
    <th>Action</th>
</tr>

{% for student in students %}

<tr>

    <td>{{ student.id }}</td>
    <td>{{ student.name }}</td>
    <td>{{ student.email }}</td>
    <td>{{ student.age }}</td>

    <td>
        <a href="{% url 'student_detail' student.id %}">
            View Details
        </a>
    </td>

</tr>

{% empty %}

<tr>
    <td colspan="5">
        No students found.
    </td>
</tr>

{% endfor %}

</table>
```

Notice we also changed:

```html
colspan="4"
```

to

```html
colspan="5"
```

because the table now has five columns.

---

## Understanding `{% url %}`

This line is today's most important concept:

```django
{% url 'student_detail' student.id %}
```

Let's break it apart.

#

### Part 1

```django
'student_detail'
```

This is **not** the URL.

It is the **URL name**.

Django searches `urls.py` for:

```python
name="student_detail"
```

and finds:

```python
path(
    "students/<int:id>/",
    ...
)
```

#

### Part 2

```django
student.id
```

This supplies the value for:

```python
<int:id>
```

Suppose:

```text
student.id = 7
```

Django generates:

```text
/students/7/
```

Automatically.

---

## What Happens During the Loop?

Suppose your database contains:

| ID | Name  |
| -- | ----- |
| 1  | John  |
| 2  | Alice |
| 3  | Bob   |

#

### First iteration

```text
student.id = 1
```

Django creates:

```html
<a href="/students/1/">
    View Details
</a>
```

#

### Second iteration

```text
student.id = 2
```

Django creates:

```html
<a href="/students/2/">
    View Details
</a>
```

#

### Third iteration

```text
student.id = 3
```

Django creates:

```html
<a href="/students/3/">
    View Details
</a>
```

You didn't write three links.

You wrote **one template**, and Django generated the correct link for every student.

---

## Why Is This Better?

Imagine six months later you change your URL.

Old:

```python
path(
    "students/<int:id>/",
    ...
)
```

New:

```python
path(
    "student/details/<int:id>/",
    ...
)
```

If you hardcoded URLs:

```html
<a href="/students/1/">
```

you'd have to search your entire project and update every link.

With:

```django
{% url 'student_detail' student.id %}
```

you only change `urls.py`.

Every template continues to work because the URL **name** hasn't changed.

This is one of Django's biggest strengths.

---

## The Complete Flow

When the user clicks **View Details**:

```text
Student List
      │
      ▼
Click View Details
      │
      ▼
{% url 'student_detail' student.id %}
      │
      ▼
Generated URL

/students/2/
      │
      ▼
urls.py
      │
      ▼
student_detail()
      │
      ▼
Database
      │
      ▼
Student Detail Page
```

---

## Test It

Run:

```bash
python manage.py runserver
```

Visit:

```text
http://127.0.0.1:8000/students/
```

You should now see:

| ID | Name  | Action       |
| -- | ----- | ------------ |
| 1  | John  | View Details |
| 2  | Alice | View Details |

Click:

**View Details**

You should be taken to the correct student's detail page.

Try it for several students and verify that each link displays the correct record.

---

## What We Learned Today

Today you learned one of Django's most frequently used template tags:

* ✅ How `{% url %}` generates URLs dynamically.
* ✅ Why URL **names** are better than hardcoded paths.
* ✅ How to pass URL parameters with `student.id`.
* ✅ How one template can generate different links for every row in a QuerySet.

You'll use `{% url %}` throughout Django—for navigation, edit buttons, delete buttons, login/logout links, and much more.

---

## 🎉 Read (Detail) Completed

At this point, you've completed the **Read** portion of CRUD:

* ✅ Read (List) — Display all students.
* ✅ Read (Detail) — Display one student.
* ✅ Safe object retrieval with `get_object_or_404()`.
* ✅ Navigation between list and detail pages using `{% url %}`.

---

## Next Lesson

According to our CRUD order, we'll now begin the next operation:

> **Update**

We'll start with the concept of updating a record and see how it's very similar to **Create**. Instead of creating a blank form, we'll learn how to **pre-fill a form with an existing student's data**, which is the foundation of every update operation in Django.
