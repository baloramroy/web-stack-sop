# Lesson 1: How a Django Request Works

## Learning Objective

By the end of this lesson, you should be able to explain:

1. What happens when a user enters a URL in the browser.
2. What `urls.py` (project) does.
3. What `urls.py` (app) does.
4. What a view is.
5. What a template is.
6. How they all work together.

---

## Big Picture

- Imagine you own a **restaurant**.
- A **customer** walks in and **asks** for a **burger**.
- The **request** doesn't go **directly** to the **chef**.
- **Instead, it follows a path.**

  ```
  Customer
      │
      ▼
  Receptionist
      │
      ▼
  Waiter
      │
      ▼
  Chef
      │
      ▼
  Food
      │
      ▼
  Customer
  ```

- **Django works almost the same way.**

  ```
  Browser
      │
      ▼
  Project URL
      │
      ▼
  App URL
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

  > This is the most important diagram in beginner Django.

---

## Let's Understand Each Part

### 1. Browser

- **Example:**

  ```
  http://127.0.0.1:8000/
  ```

  or

  ```
  http://127.0.0.1:8000/about/
  ```

  > When you press **Enter**, your browser sends an **HTTP Request**.
  

- Think of it as:

  > "Hello Django, someone wants the Home page."

#

### 2. Project `urls.py`

- **Suppose your project looks like this:**

  ```
  myproject/
  │
  ├── manage.py
  │
  ├── myproject/
  │   ├── settings.py
  │   ├── urls.py      ← Project URLs
  │   ├── wsgi.py
  │   └── asgi.py
  │
  └── myapp/
  ```

- **The browser request reaches**

  ```
  myproject/urls.py
  ```

- This file is the **main entrance** of your project.
- Think of it as the **reception desk**.
- It doesn't create **pages**.
- It only decides:

  > "Which app should handle this request?"

- **Example:**

  ```
  #Someone requests:
  > http://127.0.0.1:8000/about/
  
  #Project URL asks:
  > Which app owns `/about/`?

  ```
#

### 3. App `urls.py`

- Now Django **forwards** the request to the **app**.
  
  **Example:**

  ```
  myapp/
  │
  ├── urls.py
  ├── views.py
  ```

- This file is like the **department receptionist**.

  **It decides:**

  ```
  "/"          → home()
  "/about/"    → about()
  "/contact/"  → contact()
  ```

- It doesn't create **HTML**.
- It simply **maps** a URL to a specific **view**.

  **Think:**

  ```
  URL
  ↓

  Function
  ```

#

### 4. View (`views.py`)

- This is where the actual work happens.
- A view is simply a **Python function (or class)** that receives a request and returns a response.
- Think of the view as the **chef**.
- The chef decides:

  * What data is needed?
  * Which page should be shown?
  * What should the user receive?

- For now, don't think about databases.
- Just remember:

  ```
  Request comes in

  ↓

  View executes Python code

  ↓

  Returns a response
  ```

#

### 5. Template

- A template is simply an **HTML file**.

- **Example:**

  ```
  home.html

  about.html

  contact.html
  ```

- The template is what the user actually sees in the browser.
- Think of it as the **finished meal** served to the customer.
- The view chooses which template to return.

---

## Complete Flow

Let's follow a request from start to finish.

- **You type:**

  ```
  http://127.0.0.1:8000/about/
  ```

- **Then Django processes it like this:**

  ```
  Browser
      │
      │ Request
      ▼
  Project urls.py
      │
      ▼
  App urls.py
      │
      ▼
  View (about)
      │
      ▼
  Template (about.html)
      │
      ▼
  Browser displays HTML
  ```

Nothing is skipped.

Every request follows this path.

---

## A Real-Life Analogy

- **Imagine a company**

  ```
  Visitor
      │
      ▼
  Security Gate
      │
      ▼
  Reception
      │
      ▼
  Employee
      │
      ▼
  Prepared Document
      │
      ▼
  Visitor
  ```

- **Now compare it to Django:**

  | Company           | Django            |
  | ----------------- | ----------------- |
  | Visitor           | Browser           |
  | Security Gate     | Project `urls.py` |
  | Reception         | App `urls.py`     |
  | Employee          | View              |
  | Prepared Document | Template (HTML)   |

---

## What Each File Is Responsible For

| File               | Responsibility                                                                     |
| ------------------ | ---------------------------------------------------------------------------------- |
| `project/urls.py`  | Receives the request and sends it to the correct app.                              |
| `app/urls.py`      | Matches the requested URL to a specific view.                                      |
| `views.py`         | Contains the logic that processes the request and decides what response to return. |
| `templates/*.html` | Defines the HTML that is sent back to the browser.                                 |

---

## One Important Concept

- A common mistake beginners make is thinking:
    > "The browser opens `home.html` directly."

- **That is not how Django works.**
- The browser **never** requests a template directly.
- Instead, it requests a **URL**, and Django decides which template (if any) to render.

- The flow is always:

  ```text
  Browser
  ↓

  URL

  ↓

  View

  ↓

  Template

  ↓

  Browser
  ```

---

## What You Should Remember from This Lesson

1. The browser sends an **HTTP request**.
2. The project `urls.py` receives every request first.
3. The project `urls.py` forwards the request to the appropriate app.
4. The app `urls.py` maps the URL to a specific view.
5. The view executes Python code and prepares a response.
6. The view usually renders a template.
7. The rendered HTML is sent back to the browser.

---

