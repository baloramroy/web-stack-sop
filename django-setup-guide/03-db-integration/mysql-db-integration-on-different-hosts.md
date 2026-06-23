# SOP: Configure MySQL Database with Django instead of SQLite

We will use **MySQL** as the **backend database** on **different host**.

## Architecture Understanding

* Django App Server → runs your Django project
* MySQL DB Server → separate machine (remote)

So:

```
[Django Server]  --->  [MySQL Server:3306]
```

---

## Configure MySQL Server (Remote Side)

### Login to MySQL server:

- Run:

  ```bash
  mysql -u root -p
  ```

### Create Database

- Inside MySQL shell:

  ```sql
  CREATE DATABASE django_db;
  ```

### Allow Remote User Access

- Create user that can connect remotely:

  ```sql
  CREATE USER 'django_user'@'%' IDENTIFIED BY 'Django@123';
  ```

  > `%` = allow from any IP (we will secure later)


- Grant Privileges

  ```sql
  GRANT ALL PRIVILEGES ON django_db.* TO 'django_user'@'%';
  FLUSH PRIVILEGES;
  ```

- Exit:

  ```sql
  EXIT;
  ```

---

## Configure MySQL to Accept Remote Connections

```bash
ss -tulnp | grep 3306
Output: *:3306
```
>[!Note]
**Skip** this step if mysql service listen to **all network** like `*:3306` this.\
Otherwise **follow** below step:

- Create:

  ```bash
  vim /etc/my.cnf.d/mysql-server.cnf
  ```

- Add:

  ```ini
  [mysqld]
  bind-address = 0.0.0.0
  ```

- Restart MySQL:

  ```bash
  sudo systemctl restart mysqld
  ```

---

## Open Firewall Port (IMPORTANT)

- If firewall is active:

  ```bash
  firewall-cmd --permanent --add-port=3306/tcp
  firewall-cmd --reload
  ```

- Varify ports

  ```bash
  firewall-cmd --list-port
  ```

---

## Test Remote Access from Django Server

Install MySQL client:

```bash
dnf install mysql -y
```

Test connection:

```bash
mysql -u django_user -p -h <MYSQL_SERVER_IP> -P 3306
```

If this works → Django will work.

---

## Install Django MySQL Driver (Django Server)

Inside virtualenv:

```bash
pip install mysqlclient
```

If error:

```bash
dnf install python3-devel mysql-devel
pip install mysqlclient
```

---

## Configure Django settings.py (REMOTE DB)

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

  Replace your database config:

  ```python
  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.mysql',
          'NAME': 'django_db',
          'USER': 'django_user',
          'PASSWORD': 'StrongPassword123',
          'HOST': '<MYSQL_SERVER_IP>',   # IMPORTANT: remote IP
          'PORT': '3306',
          'OPTIONS': {
              'init_command': "SET sql_mode='STRICT_TRANS_TABLES'",
          }
      }
  }
  ```

---

## Run Migration

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

## Common Problems & Fixes


### Access denied

**Fix:**

* Check user host `%`
* Check password
* Check privileges

---

### Can’t connect to MySQL

**Check:**

- MySQL is running

  ```bash
  systemctl status mysqld
  ```

- Port open

  ```bash
  ss -tulnp | grep 3306
  ```

- Firewall open


### Django stuck / timeout

**Cause:**

* bind-address still 127.0.0.1
* firewall blocking
* wrong IP

---

## Production Security (VERY IMPORTANT)

> DO NOT use `%` in production.

- Instead:

  ```sql
  CREATE USER 'django_user'@'Django_Server_IP' IDENTIFIED BY 'StrongPassword123';
  ```

- Then:

  ```sql
  GRANT ALL PRIVILEGES ON django_db.* TO 'django_user'@'Django_Server_IP';
  ```

- Also:

  * Disable root remote login
  * Use VPN or private network
  * Restrict firewall to Django server IP only

---

