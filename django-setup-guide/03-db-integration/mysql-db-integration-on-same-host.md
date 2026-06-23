# SOP: Configure MySQL Database with Django instead of SQLite

We will use **MySQL** as the **backend database** on **same host**.

---

## Prerequisites

Make sure you already have:

1. Python installed
2. Django project created
3. Virtual environment activated
4. MySQL Installed

Check:

```bash
python --version
django-admin --version
mysql --version
```

>[!NOTE]
Refer to database installation sop.

---

## MySQL Configuration

### Login to MySQL

- Using `root` user:

  ```bash
  mysql -u root -p
  ```


### Create Database and User

- Inside MySQL shell:

  ```sql
  CREATE DATABASE django_db;
  ```

- Create user:

  ```sql
  CREATE USER 'django_user'@'localhost' IDENTIFIED BY 'Django@123';
  ```

### Provide Privileges

- Grant privileges:

  ```sql
  GRANT ALL PRIVILEGES ON django_db.* TO 'django_user'@'localhost';
  FLUSH PRIVILEGES;
  ```

- Exit:

  ```sql
  EXIT;
  ```

---

## Install MySQL Python Driver in Django Environment

- Activate your virtual environment first:

  ```bash
  source djangoenv/bin/activate
  ```

- Install driver:

  ```bash
  pip install mysqlclient
  ```

- If error occurs on Linux:

  ```bash
  dnf install python3-devel mysql-devel -y
  pip install mysqlclient
  ```

---

## Configure Django settings.py

- Open:

  ```bash
  myproject/settings.py
  ```

  > Find `DATABASES` and replace SQLite config:

- **BEFORE (SQLite)**

  ```python
  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.sqlite3',
          'NAME': BASE_DIR / 'db.sqlite3',
      }
  }
  ```


- **AFTER (MySQL)**

  ```python
  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.mysql',
          'NAME': 'django_db',
          'USER': 'django_user',
          'PASSWORD': 'StrongPassword123',
          'HOST': 'localhost',
          'PORT': '3306',
          'OPTIONS': {
              'init_command': "SET sql_mode='STRICT_TRANS_TABLES'",
          }
      }
  }
  ```

---

## Apply Migrations

Now **migrate** Django tables into **MySQL**:

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## Varify Database Migration:

To verify that the database is MySQL, check the following:

### 1. Confirm your Django database configuration

- In `settings.py`, ensure `DATABASES` looks something like:

  ```python
  DATABASES = {
      "default": {
          "ENGINE": "django.db.backends.mysql",
          "NAME": "your_database_name",
          "USER": "your_mysql_user",
          "PASSWORD": "your_password",
          "HOST": "your_mysql_server_ip",
          "PORT": "3306",
      }
  }
  ```

- The key point is:

  ```python
  "ENGINE": "django.db.backends.mysql"
  ```

- If it says:

  ```python
  "ENGINE": "django.db.backends.sqlite3"
  ```

  > then the migrations went to SQLite instead.

### 2. Verify directly in MySQL

- Log in to your MySQL server:

  ```bash
  mysql -u your_mysql_user -p
  ```

- Then run:

  ```sql
  SHOW DATABASES;
  USE your_database_name;
  SHOW TABLES;
  ```

- If the migration ran against MySQL, you should see tables such as:

  * `auth_user`
  * `auth_group`
  * `django_admin_log`
  * `django_content_type`
  * `django_migrations`
  * `django_session`

### 3. Check the migration history

- Inside MySQL:

  ```sql
  SELECT app, name FROM django_migrations;
  ```

- You should see entries like:

  ```text
  contenttypes | 0001_initial
  auth         | 0001_initial
  admin        | 0001_initial
  sessions     | 0001_initial
  ...
  ```

  > If those tables and records exist in your MySQL database, then **your Django project has successfully migrated to MySQL**.

---

## Create Superuser

- Run:

  ```bash
  python manage.py createsuperuser
  ```

---

## Run Django Server

- Run:

  ```bash
  python manage.py runserver 0.0.0.0:8000
  ```

- Check:

  ```
  http://127.0.0.1:8000/admin
  ```

---

## Common Issues & Fixes

### 1. “No module named MySQLdb”

Fix:

```bash
pip install mysqlclient
```

#

### 2. “Access denied for user”

Check:

* username/password
* privileges

#

### 3. “Can’t connect to MySQL server”

Check:

```bash
systemctl status mysqld
```

---

## Production Best Practices (Important)

* Never use root user in Django
* Use strong password
* Restrict MySQL bind-address
* Use environment variables for credentials
* Enable firewall rules for port 3306 only if remote access needed

---

