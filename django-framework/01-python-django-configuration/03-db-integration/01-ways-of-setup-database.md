>[!IMPORTANT]
If you are containerizing a Django application, the best choice to setup **database** depends on deployment architecture. Here are the common approaches.

## Option 1: Container Same Host
**Django Container + MySQL Container**\
Recommended for Development and Small Deployments


```
+----------------------+
|   Docker Host        |
|                      |
|  +----------------+  |
|  | Django         |  |
|  | Container      |  |
|  +-------+--------+  |
|          |           |
|          | Docker Network
|          |           |
|  +-------v--------+  |
|  | MySQL          |  |
|  | Container      |  |
|  +----------------+  |
+----------------------+
```

In this setup:

* Django and MySQL are attached to the same Docker network.
* Django connects to MySQL using the **container or service name**, not `localhost`.
* You **do not need to enable MySQL remote access** (`bind-address=0.0.0.0`) just for Django to connect.

Example `settings.py`:

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.mysql",
        "NAME": "myappdb",
        "USER": "myuser",
        "PASSWORD": "mypassword",
        "HOST": "mysql",      # Docker Compose service name
        "PORT": "3306",
    }
}
```

Example `docker-compose.yml`:

```yaml
services:
  web:
    build: .
    depends_on:
      - mysql

  mysql:
    image: mysql:8.4
```

Here, `HOST="mysql"` works because Docker provides internal DNS resolution.

---

## Option 2: Different Server
**Django Container or Host + MySQL Installed on a Remote Linux Server** \
Common in Production

```
+--------------------+        TCP 3306        +----------------------+
| Docker Host        | ---------------------> | Linux Server         |
|                    |                        |                      |
| +---------------+  |                        | +------------------+ |
| | Django        |  |                        | | MySQL Server     | |
| | Container     |  |                        | +------------------+ |
| +---------------+  |                        |                      |
+--------------------+                        +----------------------+
```

In this setup:

* Django runs in Docker or Host.
* MySQL runs directly on a Linux server (same machine or another server).
* Django connects using the server's IP address or hostname.

Example:

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.mysql",
        "NAME": "myappdb",
        "USER": "myuser",
        "PASSWORD": "mypassword",
        "HOST": "10.10.10.50",
        "PORT": "3306",
    }
}
```

### Do you need remote access?

**Yes**, if the MySQL server is on a different machine or if Docker cannot reach it through the loopback interface.

Typically you would:

1. Configure MySQL to listen on an appropriate interface (not just `127.0.0.1`).
2. Create a MySQL user permitted to connect from the Docker host or required network.
3. Allow TCP port `3306` through the firewall only from trusted sources.

---

## Option 3: Same Server
**Django Container or Host + MySQL on the Same Linux Host** 

Suppose:

```
Linux Host (Same Server)
├── MySQL installed normally
└── Docker
|    └── Django container
|── or Django on Linux HOst
```

If MySQL listens **only on `127.0.0.1`**, the Django container **cannot** reach it because `127.0.0.1` inside the container refers to the container itself.

You generally have two approaches:

1. Configure MySQL to listen on the host's network interface and have Django connect using the host's IP address.
2. Use Docker networking features that expose the host to containers (for example, the special hostname supported by some platforms), if appropriate for your environment.

In many production deployments, administrators instead place both services on the same private network or run both as containers.

---

## Production Recommendation

For most production environments:

```
                +----------------------+
                |     Load Balancer    |
                +----------+-----------+
                           |
                    +------+------+
                    | Django App  |
                    | (Docker)    |
                    +------+------+
                           |
                   Private Network
                           |
                    +------+------+
                    | MySQL Server |
                    | (Dedicated)  |
                    +-------------+
```

* Keep Django in containers for portability and scaling.
* Run MySQL on a dedicated VM, bare-metal server, or managed database service rather than inside the application container.
* Restrict database access to trusted hosts and networks only.
* Configure Django to use the database server's private IP address or DNS name, not `localhost`.

## Summary

| Deployment                                               | MySQL location      | Django `HOST`                                | Remote access needed?                                          |
| -------------------------------------------------------- | ------------------- | -------------------------------------------- | -------------------------------------------------------------- |
| Django + MySQL in Docker Compose                         | MySQL container     | `mysql` (service name)                       | No                                                             |
| Django in Docker + MySQL on another Linux server         | Remote Linux server | Server IP or hostname                        | Yes                                                            |
| Django in Docker + MySQL on same host but outside Docker | Host machine        | Host IP or appropriate host-network endpoint | Usually yes, unless using special host networking arrangements |

>[!NOTE]
For a Kubernetes-based production environment with Django, the typical pattern is to **run Django in pods while using an external MySQL database (or a separately managed MySQL deployment) connected over a private network**, rather than embedding MySQL inside the Django image itself.

---