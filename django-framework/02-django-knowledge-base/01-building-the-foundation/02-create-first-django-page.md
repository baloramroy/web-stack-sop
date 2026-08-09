# Lesson 2: Create Your First Django Page

## Learning Objective

By the end of this lesson, you will know how to:

1. Create an app URL configuration.
2. Connect the app to the project.
3. Create your first view.
4. Create your first template.
5. Display your first HTML page.

Just one page.

---

## Step 1: Our Project Structure

**Assume your project looks like this:**

```text
  myproject/
  │
  ├── manage.py
  │
  ├── myproject/
  │   ├── settings.py
  │   ├── urls.py
  │   └── ...
  │
  └── myapp/
      ├── views.py
      ├── models.py
      ├── admin.py
      └── ...
  ```
- **Currently, notice something.**\
  There is **no `urls.py` inside the app**.
- **That is normal.**\
  Django does **not** create one automatically.

- We must create it ourselves.

---

## Step 2: Create `myapp/urls.py`

- **Create a new file:**

  ```text
  myapp/
  │
  ├── urls.py
  ├── views.py
  ├── models.py
  └── ...
  ```

- **Add this code:**

  ```python
  from django.urls import path
  from . import views

  urlpatterns = [
  ]
  ```

#

**Let's understand every line.**

### Line 1

```python
from django.urls import path
```

- Imports Django's `path()` function.
- We'll use it to map URLs.

#

### Line 2

  ```python
  from . import views
  ```

- `. means`: Current directory of (the current app).

- This imports:
  `views.py`

- So later we can write:
  `views.home`


#

### Line 3

```python
urlpatterns = [
]
```

- This list stores **all URL mappings** for this app.
- Right now it's empty.

---

## Step 3: Create Your First View

- Open

  ```text
  myapp/views.py
  ```

- Replace or add:

  ```python
  from django.shortcuts import render

  def home(request):
      return render(request, "home.html")
  ```

  >

#

**Let's understand it**

### What is a View?

- A view is simply a Python function.

  ```python
  def home(request):
  ```

- It has:

  * Function name → `home`
  * Parameter → `request`

  > Django automatically passes the request object.

#

### What is `request`?

- When the browser visits:

  ```text
  http://127.0.0.1:8000/
  ```

  > Django creates an **HttpRequest** object.

- Think of it like a package containing information such as:

  * Requested URL
  * HTTP method (GET/POST)
  * Headers
  * Cookies
  * User information (if logged in)
  * Submitted form data

- For now, just remember:

  ```text
  Browser
  ↓

  Request object

  ↓

  View
  ```

#

### What is `render()`?

```python
return render(request, "home.html")
```

- **This means:**

  ```text
  Render the HTML template named home.html and send it back to the browser.
  ```

- Think of `render()` as:

  ```text
  Template

  ↓

  HTML

  ↓

  Browser
  ```

---

## Step 4: Add URL Mapping

- **Now go back to:**

  ```text
  myapp/urls.py
  ```

- **Update it:**

  ```python
  from django.urls import path
  from . import views

  urlpatterns = [
      path("", views.home),
  ]
  ```

- **Let's understand this line:**

  ```python
  path("", views.home)
  ```

- **It means:**

  ```text
  URL:

  /

  ↓

  Run:

  home()
  ```

  > Notice that we don't write `views.home()`.

- **We write:**

  ```python
  views.home
  ```

  > because we're **passing the function itself** to Django. Django will call it when a request matches this URL.

---

## Step 5: Connect the App to the Project

- **Open:**

  ```text
  myproject/urls.py
  ```

- **It probably looks like this:**

  ```python
  from django.contrib import admin
  from django.urls import path

  urlpatterns = [
      path("admin/", admin.site.urls),
  ]
  ```

- **Change it to:**

  ```python
  from django.contrib import admin
  from django.urls import path, include

  urlpatterns = [
      path("admin/", admin.site.urls),
      path("", include("myapp.urls")),
  ]
  ```

- New thing:

  ```python
  include("myapp.urls")
  ```

- **This tells Django:**

  ```text
  "For requests starting here (`""`), look in `myapp/urls.py` for the rest of the URL matching."
  ```

- **Now the flow becomes:**

  ```text
  Browser

  ↓

  Project urls.py

  ↓

  myapp.urls

  ↓

  home()

  ↓

  home.html
  ```

---

## Step 6: Create the Templates Folder

- **Inside your app:**

  ```text
  myapp/
  │
  ├── templates/
  ```

- **Inside it create:**

  ```text
  templates/
      home.html
  ```

- **So your app looks like:**

  ```text
  myapp/
  │
  ├── templates/
  │      └── home.html
  │
  ├── views.py
  ├── urls.py
  └── ...
  ```

---

## Step 7: Create `home.html`

- **Insert below code:**

  ```html
  <!DOCTYPE html>
  <html>
  <head>
      <title>Home</title>
  </head>
  <body>

      <h1>Welcome to Django</h1>

  </body>
  </html>
  ```

---

## Step 8: Run the Server

- **Run**

  ```bash
  python manage.py runserver
  ```

- **Visit:**

  ```text
  http://127.0.0.1:8000/
  ```

- Y**ou should see:**

  ```text
  Welcome to Django
  ```

**Congratulations!** 🎉

You've built your first Django page.

---

## Let's Follow the Request Again

◼️ **When you visit:**

```text
http://127.0.0.1:8000/
```

◼️ **This is exactly what happens:**

```text
1. Browser
       │
       ▼
2. HTTP Request
       │
       ▼
3. myproject/urls.py
       │
       ▼
4. include("myapp.urls")
       │
       ▼
5. myapp/urls.py
       │
       ▼
6. path("", views.home)
       │
       ▼
7. views.home(request)
       │
       ▼
8. render(request, "home.html")
       │
       ▼
9. Django reads home.html
       │
       ▼
10. HTML Response
       │
       ▼
11. Browser displays the page
```

---

## What Did We Learn Today

| Component             | Purpose                                                          |
| --------------------- | ---------------------------------------------------------------- |
| `views.py`            | Contains the Python logic that handles the request.              |
| `myapp/urls.py`       | Maps URLs to specific views within the app.                      |
| `myproject/urls.py`   | Delegates URL handling to the appropriate app using `include()`. |
| `templates/home.html` | Defines the HTML returned to the browser.                        |
| `render()`            | Combines a template with a request to produce an HTTP response.  |

---

## Why Create `urls.py` Inside Each App?

You might wonder why we don't put every URL in the project's `urls.py`.

- **Imagine your project grows to include:**

  ```text
  blog/
  shop/
  accounts/
  inventory/
  api/
  ```

If all URLs lived in one file, it would become large and hard to manage.

- **Instead, each app manages its own URLs:**

  ```text
  Project urls.py
  │
  ├── blog.urls
  ├── shop.urls
  ├── accounts.urls
  ├── inventory.urls
  └── api.urls
  ```

This keeps your project modular and easier to maintain.

---

