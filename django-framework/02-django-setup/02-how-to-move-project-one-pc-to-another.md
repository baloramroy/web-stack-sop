This is actually one of the most important concepts to understand. Many beginners think:

> "I pushed my Django project to GitHub, so it should run on any computer."

Not exactly. **Git only stores your project files.** It does **not** store Python itself, installed packages, virtual environments, or your database.

Let's see what actually happens.

## PC 1 (Development Computer)

Suppose you created a Django project like this:

```
myproject/
│
├── manage.py
├── requirements.txt
├── .gitignore
├── db.sqlite3 (optional)
├── myproject/
├── app/
└── venv/   ← virtual environment
```

Your virtual environment (`venv`) contains:

```
Python executable
Django
Requests
Pillow
mysqlclient
...
```

This folder is usually **NOT pushed** to Git because it is listed in `.gitignore`.

Example:

```
venv/
__pycache__/
*.pyc
```

So GitHub contains only:

```
manage.py
myproject/
app/
requirements.txt
```

---

# PC 2 (New Computer)

You clone the project.

```
git clone https://github.com/username/myproject.git
```

Now you have

```
myproject/
│
├── manage.py
├── requirements.txt
├── app/
└── myproject/
```

Notice something missing?

```
❌ venv/
```

There is no Python environment yet.

---

# Step 1 — Install Python

First make sure Python is installed.

```
python --version
```

or

```
python3 --version
```

---

# Step 2 — Create a new Virtual Environment

Inside the project folder:

Windows

```
python -m venv venv
```

Linux/macOS

```
python3 -m venv venv
```

Now you'll have

```
venv/
```

again.

---

# Step 3 — Activate it

Windows

```
venv\Scripts\activate
```

Linux/macOS

```
source venv/bin/activate
```

Prompt changes:

```
(venv) user@pc$
```

---

# Step 4 — Install all packages

This is why we create a `requirements.txt` file on PC 1.

On PC 1:

```
pip freeze > requirements.txt
```

GitHub now has

```
requirements.txt
```

Example:

```
Django==5.2.3
mysqlclient==2.2.7
Pillow==11.0.0
requests==2.32.3
```

On PC 2:

```
pip install -r requirements.txt
```

Now Django and every dependency is installed.

---

# Step 5 — Configure Environment Variables

Many projects don't store secrets in Git.

Example:

```
.env
```

contains

```
SECRET_KEY=...
DB_NAME=mydb
DB_USER=root
DB_PASSWORD=*****
```

Since `.env` is usually ignored by Git, you must create it manually on the new computer.

---

# Step 6 — Database

This depends on the database you're using.

### SQLite

If you committed

```
db.sqlite3
```

then it already exists.

If not,

```
python manage.py migrate
```

creates the database structure.

---

### MySQL/PostgreSQL

Install the database server if needed and create the database.

Example:

```
CREATE DATABASE myproject;
```

Then run

```
python manage.py migrate
```

---

# Step 7 — Run Migrations

```
python manage.py migrate
```

This creates all required tables.

---

# Step 8 — Create Superuser (optional)

If you need the Django admin:

```
python manage.py createsuperuser
```

---

# Step 9 — Run the Server

```
python manage.py runserver
```

You should see:

```
Starting development server at:

http://127.0.0.1:8000/
```

---

# What Git Does vs Doesn't Do

| Git stores       | Git does NOT store             |
| ---------------- | ------------------------------ |
| Python files     | Python installation            |
| HTML templates   | Virtual environment (`venv`)   |
| CSS/JS           | Installed packages             |
| Migrations       | Operating system               |
| Settings         | MySQL/PostgreSQL server        |
| requirements.txt | Environment variables (`.env`) |

---

# Typical Workflow Between Two PCs

### On PC 1

```bash
# Work on the project
git add .
git commit -m "Added user module"
git push
```

### On PC 2

```bash
git pull
```

If this is the **first time** setting up the project:

```bash
git clone <repo>
cd myproject

python -m venv venv
```

Activate it:

```bash
# Windows
venv\Scripts\activate

# Linux/macOS
source venv/bin/activate
```

Then:

```bash
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

---

## Production note

This process is almost exactly what happens on a production Linux server too. A deployment server typically:

1. Pulls the latest code from Git.
2. Uses (or creates) a Python virtual environment.
3. Installs dependencies from `requirements.txt`.
4. Runs `python manage.py migrate`.
5. Collects static files (if needed) with `python manage.py collectstatic`.
6. Restarts the application server (such as Gunicorn or uWSGI).

This is why `requirements.txt` and migrations are essential—they allow the project to be recreated consistently on any machine.
