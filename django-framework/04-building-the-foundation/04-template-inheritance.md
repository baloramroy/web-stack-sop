# Lesson 4: Template Inheritance (`base.html`)

## Learning Objectives

By the end of this lesson, you will understand:

1. Why template inheritance exists.
2. What `base.html` is.
3. What `{% block %}` means.
4. What `{% extends %}` means.
5. How multiple pages can share the same layout.

**Today we will NOT learn:**

* Bootstrap
* CSS
* Static files
* Database
* Models

Just template inheritance.

---

# Problem Without Template Inheritance

Right now, your templates probably look like this.

## home.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>Home</title>
</head>
<body>

<h1>Home Page</h1>

</body>
</html>
```

---

## about.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>About</title>
</head>
<body>

<h1>About Page</h1>

</body>
</html>
```

---

## contact.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>Contact</title>
</head>
<body>

<h1>Contact Page</h1>

</body>
</html>
```

Notice something?

Almost everything is repeated.

```html
<!DOCTYPE html>
<html>
<head>
...
</head>
<body>

...

</body>
</html>
```

Imagine you have:

* 20 pages
* 50 pages
* 100 pages

If you want to add a navigation bar, you'll have to edit **every file**.

That becomes a maintenance nightmare.

---

# Django's Solution

Django says:

> Put the common HTML in one file.

That file is usually called:

```text
base.html
```

Every other page **inherits** from it.

Think of it like a **master template**.

---

# Real-Life Analogy

Imagine a company letterhead.

Every letter has:

* Company logo
* Address
* Phone number

Only the **letter body** changes.

Instead of creating everything again, you use the same letterhead.

`base.html` is that letterhead.

---

# New Project Structure

Inside `templates/`:

```text
templates/
│
├── base.html
├── home.html
├── about.html
└── contact.html
```

---

# Step 1: Create `base.html`

Create:

```text
templates/base.html
```

Put this inside:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Django Learning</title>
</head>
<body>

    <h1>My Django Website</h1>

    <hr>

    {% block content %}

    {% endblock %}

</body>
</html>
```

Let's understand every part.

---

## This Part

```html
<!DOCTYPE html>
<html>
<head>
```

Appears on every page.

So it belongs in `base.html`.

---

## This

```html
<h1>My Django Website</h1>
```

This is your site's main heading.

Every page should display it.

So it also belongs in `base.html`.

---

## This

```html
<hr>
```

A horizontal line.

Again, common to every page.

---

# The Magic Part

```django
{% block content %}

{% endblock %}
```

This is called a **block**.

Think of it as:

> "Child templates can insert their own content here."

It is like leaving an empty space in a document.

---

Imagine this:

```text
========================

Company Header

------------------------

(Empty Space)

========================
```

Every page fills that empty space differently.

---

# Step 2: Update `home.html`

Replace everything with:

```django
{% extends "base.html" %}

{% block content %}

<h2>Home Page</h2>

<p>Welcome to my Django website.</p>

{% endblock %}
```

Much smaller!

---

# Step 3: Update `about.html`

```django
{% extends "base.html" %}

{% block content %}

<h2>About Page</h2>

<p>This is the about page.</p>

{% endblock %}
```

---

# Step 4: Update `contact.html`

```django
{% extends "base.html" %}

{% block content %}

<h2>Contact Page</h2>

<p>Contact us here.</p>

{% endblock %}
```

---

# What Does `{% extends %}` Mean?

```django
{% extends "base.html" %}
```

It means:

> "Start with `base.html`, then replace its blocks with my content."

The child template does **not** need to rewrite the HTML structure.

---

# What Django Does Behind the Scenes

Suppose `base.html` is:

```html
<html>
<body>

Header

{% block content %}
{% endblock %}

Footer

</body>
</html>
```

And `home.html` is:

```django
{% extends "base.html" %}

{% block content %}

Home Page

{% endblock %}
```

Django combines them into this final HTML:

```html
<html>
<body>

Header

Home Page

Footer

</body>
</html>
```

The browser **never sees** `{% extends %}` or `{% block %}`. Those are Django Template Language (DTL) tags processed on the server before the HTML is sent to the browser.

---

# Visualizing It

```
base.html

+----------------------+
| Header               |
|                      |
| Block Content        |
|                      |
| Footer               |
+----------------------+
```

↓

```
home.html

+----------------------+
| Home Page            |
| Welcome...           |
+----------------------+
```

↓

```
Browser

+----------------------+
| Header               |
|                      |
| Home Page            |
| Welcome...           |
|                      |
| Footer               |
+----------------------+
```

---

# Let's Improve `base.html`

Now add simple navigation.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Django Learning</title>
</head>
<body>

<h1>My Django Website</h1>

<hr>

<a href="/">Home</a>

<a href="/about/">About</a>

<a href="/contact/">Contact</a>

<hr>

{% block content %}

{% endblock %}

</body>
</html>
```

Visit all three pages.

You'll notice:

* Same heading
* Same navigation
* Same layout

Only the page content changes.

This is exactly why template inheritance exists.

---

# One Small Issue

Right now, our links are **hardcoded**:

```html
<a href="/about/">About</a>
```

This works, but it's **not the Django way**.

Remember in the last lesson we gave our URLs names?

```python
path("about/", views.about, name="about")
```

Next, use those names instead:

```django
<a href="{% url 'about' %}">About</a>
```

Similarly:

```django
<a href="{% url 'home' %}">Home</a>

<a href="{% url 'about' %}">About</a>

<a href="{% url 'contact' %}">Contact</a>
```

Now Django looks up the URL by its **name**, not by a hardcoded path.

If you later change:

```python
path("about/", ...)
```

to

```python
path("company/about-us/", ...)
```

you don't have to edit `base.html`. `{% url 'about' %}` will automatically generate the new path.

This is why URL names are so valuable.

---

# Summary

You learned four important concepts today:

| Concept                     | Purpose                                                       |
| --------------------------- | ------------------------------------------------------------- |
| `base.html`                 | Holds the common layout shared by multiple pages.             |
| `{% extends "base.html" %}` | Makes a template inherit from `base.html`.                    |
| `{% block content %}`       | Defines a section that child templates can override.          |
| `{% url 'name' %}`          | Generates URLs using their names instead of hardcoding paths. |

---

# Homework

Before moving on, make sure you can answer these questions:

1. Why do we create `base.html`?
2. What is the difference between `base.html` and `home.html`?
3. Why does `home.html` not need `<html>`, `<head>`, or `<body>` anymore?
4. What does `{% extends "base.html" %}` do?
5. Why is `{% url 'about' %}` better than `href="/about/"`?

---
