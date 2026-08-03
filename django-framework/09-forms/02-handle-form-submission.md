Perfect. We'll stay consistent with the roadmap.

You have completed:

* ✅ Step 29 — Create Forms

Now we'll start:

# **Phase 8 — Forms**

## **Step 30 — Handle Form Submission**

This is one of the most important concepts in Django because it explains the complete lifecycle of a form.

---

# Learning Objective

By the end of this lesson, you'll understand:

* How a browser requests a form
* How Django displays the form
* What happens when the user clicks **Submit**
* How Django receives submitted data
* How to validate it
* How to process it

We are **not** building a real project yet. The goal is to understand the workflow first.

---

# The Big Picture

A Django form usually has **two jobs**, handled by the **same view**.

## First Request (GET)

The user visits

```
/contact/
```

Browser sends

```
GET /contact/
```

Django returns

```
Empty form
```

The browser displays

```
Name:  __________

Email: __________

[Submit]
```

Nothing has been submitted yet.

---

# Second Request (POST)

The user types

```
Name: John

Email: john@gmail.com
```

Then clicks

```
Submit
```

Now the browser sends

```
POST /contact/
```

Notice that the page URL is often the same.

Before

```
GET /contact/
```

After clicking Submit

```
POST /contact/
```

The difference is **not the URL**.

The difference is the **HTTP method**.

---

# Visual Flow

```
User opens page
        │
        ▼
GET request
        │
        ▼
View creates empty form
        │
        ▼
Template displays form
        │
        ▼
User fills form
        │
        ▼
Clicks Submit
        │
        ▼
POST request
        │
        ▼
View receives submitted data
        │
        ▼
Validation
        │
        ▼
Valid?
 ┌─────────────┐
 │             │
 │ Yes         │ No
 │             │
 ▼             ▼
Process     Show errors
```

---

# Why GET First?

Think of ordering food online.

First

You open the ordering page.

Nothing has been ordered.

This is

```
GET
```

Then

You choose items.

Click

```
Place Order
```

Now information is sent.

That's

```
POST
```

---

# How Django Knows?

Inside the view, Django checks

```python
request.method
```

It can be

```
GET
```

or

```
POST
```

Example

```python
if request.method == "POST":
    print("User submitted the form")
else:
    print("Display empty form")
```

You don't need to memorize this yet—just understand the idea.

---

# Where Does the Submitted Data Go?

When the browser submits a form, Django stores the submitted values in

```python
request.POST
```

Example

Suppose the user enters

```
Name: John
Email: john@gmail.com
```

Then

```python
request.POST
```

contains something conceptually like

```text
{
    "name": "John",
    "email": "john@gmail.com"
}
```

This is how Django accesses submitted form data.

---

# How Forms Use This Data

Instead of manually reading `request.POST`, Django forms can take it directly.

Conceptually:

```python
form = ContactForm(request.POST)
```

The form now contains the user's submitted values and can validate them.

---

# Validation

Once the form has the submitted data, Django checks:

* Is every required field filled?
* Is the email valid?
* Is the data the correct type?
* Does it satisfy any custom rules?

If everything is correct:

```
Valid
```

If something is wrong:

```
Invalid
```

The form remembers the user's input and any error messages so they can be shown back on the page.

---

# The Complete Lifecycle

```
Browser
   │
   ▼
GET
   │
   ▼
View
   │
   ▼
Create Empty Form
   │
   ▼
Template
   │
   ▼
User fills form
   │
   ▼
POST
   │
   ▼
View
   │
   ▼
Create Form with POST data
   │
   ▼
Validation
   │
   ├──────────► Invalid
   │               │
   │               ▼
   │         Show form again
   │
   ▼
Valid
   │
   ▼
Save data / Send email / Process
   │
   ▼
Response
```

---

# Key Concepts to Remember

* **GET** is used to display an empty form.
* **POST** is used to submit form data.
* `request.method` tells Django whether the request is GET or POST.
* Submitted data is available in `request.POST`.
* A Django form uses that data to perform validation.
* If the data is valid, you process it.
* If it's invalid, you show the form again with errors.

---

## ✅ Step 30 Summary

You now understand the complete flow of handling a form submission:

1. Browser sends a **GET** request.
2. Django returns an empty form.
3. The user fills in the form.
4. Browser sends a **POST** request.
5. Django receives the submitted data.
6. The form validates the data.
7. If valid, Django processes it; if not, it redisplays the form with errors.

We still haven't connected a form to a view or template in code. That comes next, where you'll apply this lifecycle step by step before moving on to **Step 31 — Validation**.
