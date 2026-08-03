**Phase 8 — Forms**

# Step 3 (Practical) — Display and Submit a Form

You have completed:

* ✅ Step 1 — Create Forms
* ✅ Step 2 — Handle Form Submission (Concept)

Now we'll move to the **practical implementation** of Step 2.

> **Goal of this lesson:** Connect a form to a view and template so you can display it and receive submitted data. We **won't validate or save** the data yet—that is the focus of Step 4.

---


Until now, our form only existed as a Python class.

```python
class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
```

A Python class alone cannot appear in a browser.

We need Django to connect three pieces:

```
Form
   │
   ▼
View
   │
   ▼
Template
   │
   ▼
Browser
```

---

## Overall Flow

This is what we're going to build.

```
User
 │
 │ visits /contact/
 ▼
View
 │
 │ creates ContactForm()
 ▼
Template
 │
 │ displays HTML form
 ▼
Browser

User fills form

Clicks Submit

Browser
 │
 │ POST
 ▼
View
 │
 │ receives submitted data
 ▼
Print submitted data
```

Notice that we're **not validating or saving anything yet**.

---

## Step 1 — The View

Open

```
views.py
```

Import the form.

```python
from .forms import ContactForm
```

Now create a view.

```python
from django.shortcuts import render
from .forms import ContactForm


def contact(request):
    form = ContactForm()

    return render(request, "contact.html", {
        "form": form
    })
```

Let's understand every line.

#

### `request`

```python
def contact(request):
```

Whenever someone visits

```
/contact/
```

Django calls this function.

The `request` object contains information about the incoming HTTP request.

For now, just remember:

```
Browser
     │
     ▼
request
```

#

### Create the Form

```python
form = ContactForm()
```

This creates an **empty** form.

Think of it like this:

```
Name:
Email:
```

Nothing has been filled in yet.

#

### Send Form to Template

```python
return render(
    request,
    "contact.html",
    {
        "form": form
    }
)
```

The template now has access to a variable called:

```
form
```

---

## Step 2 — URL

Open

```
urls.py
```

Add the route.

```python
from django.urls import path
from . import views

urlpatterns = [
    path("contact/", views.contact, name="contact"),
]
```

Now Django knows:

```
/contact/
        │
        ▼
views.contact
```

---

## Step 3 — Template

Create

```
templates/contact.html
```

Write

```html
<!DOCTYPE html>
<html>
<head>
    <title>Contact Form</title>
</head>
<body>

<h1>Contact Form</h1>

<form>
    {{ form }}

    <button type="submit">
        Submit
    </button>
</form>

</body>
</html>
```

Run the server.

Visit

```
http://127.0.0.1:8000/contact/
```

You should now see:

```
Name
[____________]

Email
[____________]

[Submit]
```

Congratulations!

This is your **first Django form rendered in a browser**.

---

## What Does `{{ form }}` Do?

This line

```django
{{ form }}
```

tells Django:

> "Render every field in this form."

Conceptually, Django generates HTML similar to this:

```html
<label>Name:</label>
<input type="text">

<label>Email:</label>
<input type="email">
```

You didn't write that HTML yourself.

Django generated it from the `ContactForm` class.

---

## What Happens When Submit Is Clicked?

Right now:

```
User
 │
 ▼
Submit
```

The browser submits the form.

But where?

Because we didn't specify:

```html
action=""
```

the browser submits the form back to the **same URL**.

```
/contact/
```

---

## Something Is Missing

Our current form is:

```html
<form>
```

It doesn't tell the browser which HTTP method to use.

By default, browsers use:

```
GET
```

That means if someone enters:

```
Name = John
Email = john@gmail.com
```

the browser may send a URL like:

```
/contact/?name=John&email=john@gmail.com
```

That is **not** how we usually submit forms that create or update data.

For forms that send user-entered data, we normally use **POST**.

Update the form tag:

```html
<form method="post">
```

Now the browser will send a POST request instead of a GET request.

---

## CSRF Protection

When using POST in Django, you must include a CSRF token.

Add this inside the form:

```html
<form method="post">
    {% csrf_token %}

    {{ form }}

    <button type="submit">
        Submit
    </button>
</form>
```

Your complete template becomes:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Contact Form</title>
</head>
<body>

<h1>Contact Form</h1>

<form method="post">
    {% csrf_token %}

    {{ form }}

    <button type="submit">
        Submit
    </button>
</form>

</body>
</html>
```

The `{% csrf_token %}` tag helps protect your application from a type of attack called **Cross-Site Request Forgery (CSRF)**. For now, simply remember this rule:

> **If your Django form uses `method="post"`, always include `{% csrf_token %}` inside the `<form>` element.**

We'll study CSRF in detail in a later security phase.

---

## Receiving the Submitted Data

Now modify the view.

```python
from django.shortcuts import render
from .forms import ContactForm


def contact(request):

    if request.method == "POST":
        print(request.POST)

    form = ContactForm()

    return render(request, "contact.html", {
        "form": form
    })
```

Now:

1. Open the page.
2. Fill the form.
3. Click **Submit**.

Your terminal will print something similar to:

```text
<QueryDict: {
    'csrfmiddlewaretoken': '...',
    'name': ['John'],
    'email': ['john@gmail.com']
}>
```

This shows that Django has successfully received the submitted data.

We're **not** validating it yet—we're simply confirming that the browser sent the data and the view received it.

---

## Request Lifecycle

```
Browser
    │
    │ GET
    ▼
View
    │
    ▼
Create ContactForm()
    │
    ▼
Template
    │
    ▼
Display Form
    │
User enters data
    │
Clicks Submit
    │
    │ POST
    ▼
View
    │
    ▼
request.POST
    │
    ▼
Print data
```

---

## Common Beginner Mistakes

### Forgetting `method="post"`

```html
<form>
```

The browser sends a GET request instead of POST.

#

### Forgetting `{% csrf_token %}`

With `method="post"` but no CSRF token, Django will reject the request with a **403 Forbidden** error.

#

### Forgetting to pass the form to the template

```python
return render(request, "contact.html")
```

Then `{{ form }}` doesn't exist in the template.

Always pass it:

```python
return render(request, "contact.html", {
    "form": form
})
```

---

## Step 3 (Practical) Summary

You have now connected all the essential pieces:

* ✅ Created a view that instantiates the form.
* ✅ Added a URL to access the view.
* ✅ Rendered the form in a template using `{{ form }}`.
* ✅ Used `method="post"` for form submission.
* ✅ Added `{% csrf_token %}` for Django's CSRF protection.
* ✅ Received the submitted data through `request.POST`.

At this point, the form can be displayed and submitted. The next step is to **validate** that submitted data using Django's form system, which is exactly what we'll cover in **Step 4 — Validation**.
