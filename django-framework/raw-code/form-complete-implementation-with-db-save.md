# Add Student Form - Complete Implementation with Database Save

## File Structure
```
myapp/
├── templates/
│   └── myapp/
│       └── student_form.html
├── models.py
├── views.py
├── urls.py
├── admin.py
└── myproject/
    └── urls.py
```

---

## 1. Model
**`myapp/models.py`**
```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name
```

---

## 2. Admin Registration
**`myapp/admin.py`**
```python
from django.contrib import admin
from .models import Student

admin.site.register(Student)
```

---

## 3. Template
**`myapp/templates/myapp/student_form.html`**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Add Student</title>
</head>
<body>

    <h1>Add Student</h1>

    {% if messages %}
        {% for message in messages %}
            <p style="color: green;">{{ message }}</p>
        {% endfor %}
    {% endif %}

    <form method="POST">
        {% csrf_token %}

        <p>
            <label>Name</label><br>
            <input type="text" name="name" required>
        </p>

        <p>
            <label>Email</label><br>
            <input type="email" name="email" required>
        </p>

        <p>
            <label>Age</label><br>
            <input type="number" name="age" required>
        </p>

        <button type="submit">
            Save
        </button>
    </form>

    <br>
    <a href="/students/">View All Students</a>

</body>
</html>
```

---

## 4. Views
**`myapp/views.py`**
```python
from django.shortcuts import render, redirect
from django.contrib import messages
from .models import Student

def student_create(request):
    if request.method == "POST":
        name = request.POST.get("name")
        email = request.POST.get("email")
        age = request.POST.get("age")

        student = Student.objects.create(
            name=name,
            email=email,
            age=age
        )

        messages.success(request, f"Student {student.name} added successfully!")
        return redirect("student_create")

    return render(request, "myapp/student_form.html")

def student_list(request):
    students = Student.objects.all()
    return render(request, "myapp/student_list.html", {"students": students})
```

---

## 5. Student List Template
**`myapp/templates/myapp/student_list.html`**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Student List</title>
</head>
<body>

    <h1>Student List</h1>

    <a href="/students/add/">Add New Student</a>

    <br><br>

    {% if students %}
        <table border="1">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Email</th>
                    <th>Age</th>
                    <th>Created</th>
                </tr>
            </thead>
            <tbody>
                {% for student in students %}
                <tr>
                    <td>{{ student.id }}</td>
                    <td>{{ student.name }}</td>
                    <td>{{ student.email }}</td>
                    <td>{{ student.age }}</td>
                    <td>{{ student.created_at }}</td>
                </tr>
                {% endfor %}
            </tbody>
        </table>
    {% else %}
        <p>No students found.</p>
    {% endif %}

</body>
</html>
```

---

## 6. App URLs
**`myapp/urls.py`**
```python
from django.urls import path
from . import views

urlpatterns = [
    path("students/add/", views.student_create, name="student_create"),
    path("students/", views.student_list, name="student_list"),
]
```

---

## 7. Project URLs
**`myproject/urls.py`**
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),
]
```

---

## 8. Migrations
```bash
python manage.py makemigrations
python manage.py migrate
```

---

## 9. Run Server
```bash
python manage.py runserver
```

---

## 10. Access Pages
```
Add Student:    http://127.0.0.1:8000/students/add/
View Students:  http://127.0.0.1:8000/students/
Admin Panel:    http://127.0.0.1:8000/admin/
```