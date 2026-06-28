# Lesson 3: Multiple Pages & URL Routing

## Learning Objectives

By the end of this lesson, you will understand:

1. How to create multiple views.
2. How to map different URLs to different views.
3. Why every URL usually has its own view.
4. How the request changes when the URL changes.
5. (New Concept) URL Names.

---

## Step 1: The Goal

- **We want this:**

  | URL         | View        | Template       |
  | ----------- | ----------- | -------------- |
  | `/`         | `home()`    | `home.html`    |
  | `/about/`   | `about()`   | `about.html`   |
  | `/contact/` | `contact()` | `contact.html` |

  Notice the pattern.

- **Each URL points to:**
  > One URL → One View → One Template

---

## Step 2: Create Two More Templates

- Inside:

  ```text
  myapp/templates/
  ```

- Create:

  ```text
  home.html
  about.html
  contact.html
  ```

---

### home.html

- **Already created this before:**

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

### about.html

- **Create this one:**

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

### contact.html

- **Create this one too:**

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

---

## Step 3: Create More Views

- **Open:**

  ```text
  views.py
  ```

- **Now write:**

  ```python
  from django.shortcuts import render

  def home(request):
      return render(request, "home.html")

  def about(request):
      return render(request, "about.html")

  def contact(request):
      return render(request, "contact.html")
  ```

- **Let's understand what's happening.**

  * We now have **three Python functions**.

  * Each function is responsible for **one page only**.

- **Think of it like this:**

  ```
  home()    → Home page

  about()   → About page

  contact() → Contact page
  ```

---

## Step 4: Update `urls.py`

- **Open:**

  ```text
  myapp/urls.py
  ```

- **Update it:**

  ```python
  from django.urls import path
  from . import views

  urlpatterns = [
      path("", views.home),

      path("about/", views.about),

      path("contact/", views.contact),
  ]
  ```


---

### Let's understand each line

- **First URL**

  ```python
  path("", views.home)
  ```

  Matches:

  ```
  http://127.0.0.1:8000/
  ```

#

- **Second URL**

  ```python
  path("about/", views.about)
  ```

  Matches:

  ```
  http://127.0.0.1:8000/about/
  ```

#

- **Third URL**

  ```python
  path("contact/", views.contact)
  ```

  Matches:

  ```
  http://127.0.0.1:8000/contact/
  ```

---

### Visualizing URL Matching

- **Imagine Django reads the URLs from top to bottom.**

  ```
  User requests:

  /about/

  ↓

  Check first rule

  ""

  No match

  ↓

  Check second rule

  "about/"

  Match found ✅

  ↓

  Run

  views.about()

  ↓

  Render about.html
  ```

#

- **Another example:**

  ```
  User requests:

  /contact/

  ↓

  Check ""

  No

  ↓

  Check "about/"

  No

  ↓

  Check "contact/"

  Yes ✅

  ↓

  views.contact()

  ↓

  contact.html
  ```

---

## Step 5: Test Everything

- **Run:**

  ```bash
  python manage.py runserver
  ```

- **Visit:**

  ```
  http://127.0.0.1:8000/
  ```

- **Output:**

  ```
  Home Page
  ```

#

- **Visit:**

  ```
  http://127.0.0.1:8000/about/
  ```

- **Output:**

  ```
  About Page
  ```

#

- **Visit:**

  ```
  http://127.0.0.1:8000/contact/
  ```

- **Output:**

  ```
  Contact Page
  ```

>Congratulations! 🎉\
>You now have a mini website with three pages.

---

## New Concept: URL Names

- So far, our URLs look like this:

  ```python
  urlpatterns = [
      path("", views.home),

      path("about/", views.about),

      path("contact/", views.contact),
  ]
  ```

  > This works, but Django encourages us to **name our URLs**.

- Update it to:

  ```python
  urlpatterns = [
      path("", views.home, name="home"),

      path("about/", views.about, name="about"),

      path("contact/", views.contact, name="contact"),
  ]
  ```

#

### What is `name`?

- The `name` is a unique identifier for a URL.
- Think of it like a **nickname**.
- Instead of saying:
  > "Go to `/about/`"

- you can say:
  > "Go to the URL named `about`."

---

## Why Use URL Names?

- Imagine you hardcode links in many templates:

  ```html
  <a href="/about/">About</a>
  ```

- Later, your manager says:
  ```
  Change the URL from /about/ to /company/about-us/.
  ```
  > Without **URL names**, you must update every **hardcoded** link.

- With URL names, you only change one place:

  ```python
  path("company/about-us/", views.about, name="about")
  ```

  - Every link that uses the name `"about"` will automatically point to the new URL.

  - This is one of Django's strengths: **you reference URLs by name instead of by hardcoded paths**.

---

## Summary

Here's what you learned today:

| URL         | View        | Template       | URL Name  |
| ----------- | ----------- | -------------- | --------- |
| `/`         | `home()`    | `home.html`    | `home`    |
| `/about/`   | `about()`   | `about.html`   | `about`   |
| `/contact/` | `contact()` | `contact.html` | `contact` |

---

## Request Flow Example

- When you visit:

  ```
  http://127.0.0.1:8000/contact/
  ```

- The flow is:

  ```
  Browser
      │
      ▼
  Project urls.py
      │
      ▼
  App urls.py
      │
      ▼
  path("contact/", views.contact)
      │
      ▼
  views.contact(request)
      │
      ▼
  render(request, "contact.html")
      │
      ▼
  Browser displays Contact Page
  ```

---

## Homework (Hands-on)

Before we move to the next lesson, I want you to do three small tasks on your own:

1. Create a new page called **Services**:

   * URL: `/services/`
   * View: `services()`
   * Template: `services.html`
   * URL name: `services`

2. Create another page called **Profile**:

   * URL: `/profile/`
   * View: `profile()`
   * Template: `profile.html`
   * URL name: `profile`

3. Visit all five pages in your browser and verify that each displays its correct heading.

---
