**Phase 5 → CRUD**

# Topic: Read (List) - Handle Empty List


So far, you've learned:

* ✅ `Student.objects.all()`
* ✅ Passing a QuerySet to a template
* ✅ `{% for student in students %}`
* ✅ Displaying data in an HTML table

Today we'll improve our page by handling the case where **no students exist**.

---

## Today's Goal

Suppose your database has **no records**.

Your current page displays:

| ID | Name | Email | Age |
| -- | ---- | ----- | --- |

That's it.

The user doesn't know whether:

* the page is broken,
* the database failed,
* or there are simply no students.

A better application should tell the user what's happening.

---

## The Problem

Our current template is:

```django
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

What happens if:

```python
Student.objects.all()
```

returns **zero records**?

The loop simply runs **zero times**.

Only the table header is displayed.

---

## How Django Solves This

Django's template language provides a special clause:

```django
{% empty %}
```

It works together with a `for` loop.

General syntax:

```django
{% for item in items %}

    ...

{% empty %}

    ...

{% endfor %}
```

Read it like English:

> "Loop through the items. If there aren't any, execute the `{% empty %}` block."

---

## Step 1 — Update the Template

Replace your loop with:

```html
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

    {% empty %}

    <tr>
        <td colspan="4">
            No students found.
        </td>
    </tr>

    {% endfor %}

</table>
```

Notice the new part:

```django
{% empty %}

<tr>
    <td colspan="4">
        No students found.
    </td>
</tr>
```

---

## Understanding `colspan="4"`

Our table has four columns:

```text
ID
Name
Email
Age
```

Normally, each row has four `<td>` cells.

But our message should stretch across the whole table.

That's why we write:

```html
<td colspan="4">
```

which means:

> "This single cell should span all four columns."

Without `colspan`, the message would only appear under the first column, making the table look broken.

---

## What Happens Internally?

### Case 1 — Students Exist

Suppose the database contains:

| ID | Name  |
| -- | ----- |
| 1  | John  |
| 2  | Alice |

The flow is:

```text
Student.objects.all()
        │
        ▼
2 Students
        │
        ▼
for loop
        │
        ▼
John
Alice
```

The `{% empty %}` block is ignored.

#

### Case 2 — Database Is Empty

Suppose the database contains:

```text
0 Students
```

Now the flow becomes:

```text
Student.objects.all()
        │
        ▼
Empty QuerySet
        │
        ▼
for loop
        │
        ▼
No iterations
        │
        ▼
Execute {% empty %}
        │
        ▼
"No students found."
```

The loop body is skipped, and Django renders the `{% empty %}` section instead.

---

## What You'll See

### Before

```text
Student List

+----+------+-------+------+
| ID | Name | Email | Age  |
+----+------+-------+------+
```

The page looks unfinished.

#

### After

```text
Student List

+----+-------------------------+
| ID | Name | Email | Age      |
+----+-------------------------+
|     No students found.       |
+------------------------------+
```

Now the user immediately understands that the application is working—there just aren't any records yet.

---

## Why Is This Better Than Using `{% if %}`?

You might wonder why we don't write:

```django
{% if students %}
```

You certainly can, and we'll learn `{% if %}` in other situations.

However, when you're already looping through data, Django provides `{% empty %}` because it keeps everything in one place:

```django
{% for student in students %}
    ...
{% empty %}
    ...
{% endfor %}
```

This is cleaner, easier to read, and is the pattern you'll commonly see in Django projects.

---

## The Complete Read (List) Flow

```text
Browser
      │
      ▼
/students/
      │
      ▼
student_list()
      │
      ▼
Student.objects.all()
      │
      ▼
QuerySet
      │
      ▼
Template
      │
      ├── Has records?
      │      │
      │      ├── Yes → Display each student
      │      │
      │      └── No → Display "No students found."
      │
      ▼
Browser
```

---

## What We Learned Today

Today you learned:

* ✅ How `{% empty %}` works with a Django `for` loop.
* ✅ Why it provides a better user experience when there are no records.
* ✅ How `colspan` lets one table cell span multiple columns.
* ✅ How Django decides whether to execute the loop body or the `{% empty %}` block.

This is a small feature, but it's part of writing user-friendly Django applications.

---

## Next Lesson

We've now completed the basic **Read (List)** functionality.

The next topic in your roadmap is:

> **Read (Detail)**

You'll learn how to display **one specific student** by its ID. This introduces URL parameters, retrieving a single object from the database, and building a dedicated detail page such as:

```text
/students/1/
```

where Django displays the complete information for exactly one student.
