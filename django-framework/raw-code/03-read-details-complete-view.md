# Complete Read (Detail) Feature - End to End Code

Here's the complete implementation for the Read (Detail) feature with all files you need.

---

## File Structure
```
myapp/
├── models.py
├── views.py
├── urls.py
├── templates/
│   └── myapp/
│       ├── student_list.html
│       └── student_detail.html
└── migrations/
    └── __init__.py
```

---

## 1. models.py
```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    age = models.IntegerField()
    
    def __str__(self):
        return self.name
```

---

## 2. urls.py
```python
from django.urls import path
from . import views

urlpatterns = [
    # Read (List) - Display all students
    path(
        "students/",
        views.student_list,
        name="student_list"
    ),
    
    # Read (Detail) - Display single student
    path(
        "students/<int:id>/",
        views.student_detail,
        name="student_detail"
    ),
    
    # Create
    path(
        "students/add/",
        views.student_create,
        name="student_create"
    ),
]
```

---

## 3. views.py
```python
from django.shortcuts import render, redirect, get_object_or_404
from .models import Student

# READ (LIST) - Display all students
def student_list(request):
    students = Student.objects.all()
    return render(
        request,
        "myapp/student_list.html",
        {
            "students": students
        }
    )

# READ (DETAIL) - Display one student
def student_detail(request, id):
    student = get_object_or_404(
        Student,
        id=id
    )
    return render(
        request,
        "myapp/student_detail.html",
        {
            "student": student
        }
    )

# CREATE
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
        return redirect("student_list")
    
    return render(
        request,
        "myapp/student_create.html"
    )
```

---

## 4. templates/myapp/student_list.html
```html
<!DOCTYPE html>
<html>
<head>
    <title>Student List</title>
    <style>
        table {
            border-collapse: collapse;
            width: 80%;
            margin: 20px auto;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 12px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
        .add-btn {
            display: block;
            width: 150px;
            margin: 20px auto;
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            text-align: center;
            text-decoration: none;
            border-radius: 4px;
        }
        .add-btn:hover {
            background-color: #45a049;
        }
        .view-link {
            color: #2196F3;
            text-decoration: none;
        }
        .view-link:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>

    <h1 style="text-align: center;">Student List</h1>

    <a href="{% url 'student_create' %}" class="add-btn">
        + Add New Student
    </a>

    <table>
        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Email</th>
            <th>Age</th>
            <th>Action</th>
        </tr>

        {% for student in students %}
        <tr>
            <td>{{ student.id }}</td>
            <td>{{ student.name }}</td>
            <td>{{ student.email }}</td>
            <td>{{ student.age }}</td>
            <td>
                <a href="{% url 'student_detail' student.id %}" class="view-link">
                    View Details
                </a>
            </td>
        </tr>
        {% empty %}
        <tr>
            <td colspan="5" style="text-align: center;">
                No students found. 
                <a href="{% url 'student_create' %}">Add one now</a>
            </td>
        </tr>
        {% endfor %}
    </table>

</body>
</html>
```

---

## 5. templates/myapp/student_detail.html
```html
<!DOCTYPE html>
<html>
<head>
    <title>Student Details</title>
    <style>
        .container {
            width: 50%;
            margin: 50px auto;
            padding: 30px;
            border: 1px solid #ddd;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        h1 {
            color: #333;
            text-align: center;
        }
        .detail-row {
            display: flex;
            padding: 12px 0;
            border-bottom: 1px solid #eee;
        }
        .label {
            font-weight: bold;
            width: 100px;
            color: #555;
        }
        .value {
            flex: 1;
            color: #333;
        }
        .back-link {
            display: block;
            text-align: center;
            margin-top: 20px;
            color: #2196F3;
            text-decoration: none;
        }
        .back-link:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Student Details</h1>

        <div class="detail-row">
            <div class="label">ID:</div>
            <div class="value">{{ student.id }}</div>
        </div>

        <div class="detail-row">
            <div class="label">Name:</div>
            <div class="value">{{ student.name }}</div>
        </div>

        <div class="detail-row">
            <div class="label">Email:</div>
            <div class="value">{{ student.email }}</div>
        </div>

        <div class="detail-row">
            <div class="label">Age:</div>
            <div class="value">{{ student.age }}</div>
        </div>

        <a href="{% url 'student_list' %}" class="back-link">
            ← Back to Student List
        </a>
    </div>

</body>
</html>
```

---

## 6. templates/myapp/student_create.html
```html
<!DOCTYPE html>
<html>
<head>
    <title>Add Student</title>
    <style>
        .container {
            width: 50%;
            margin: 50px auto;
            padding: 30px;
            border: 1px solid #ddd;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        h1 {
            color: #333;
            text-align: center;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            font-weight: bold;
            margin-bottom: 5px;
            color: #555;
        }
        input[type="text"],
        input[type="email"],
        input[type="number"] {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        .submit-btn {
            width: 100%;
            padding: 12px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        .submit-btn:hover {
            background-color: #45a049;
        }
        .back-link {
            display: block;
            text-align: center;
            margin-top: 15px;
            color: #2196F3;
            text-decoration: none;
        }
        .back-link:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Add New Student</h1>

        <form method="POST">
            {% csrf_token %}
            
            <div class="form-group">
                <label for="name">Name:</label>
                <input type="text" id="name" name="name" required>
            </div>

            <div class="form-group">
                <label for="email">Email:</label>
                <input type="email" id="email" name="email" required>
            </div>

            <div class="form-group">
                <label for="age">Age:</label>
                <input type="number" id="age" name="age" required>
            </div>

            <button type="submit" class="submit-btn">
                Add Student
            </button>
        </form>

        <a href="{% url 'student_list' %}" class="back-link">
            ← Back to Student List
        </a>
    </div>

</body>
</html>
```

---

## 7. Database Migration Commands
```bash
# Create migration files
python manage.py makemigrations

# Apply migrations to database
python manage.py migrate
```

---

## 8. Test Data (Optional - Add via Django Shell)
```bash
python manage.py shell
```

```python
from myapp.models import Student

# Create test students
Student.objects.create(name="John", email="john@example.com", age=22)
Student.objects.create(name="Alice", email="alice@example.com", age=21)
Student.objects.create(name="Bob", email="bob@example.com", age=24)

# Verify
Student.objects.all()
```

---

## 9. Run the Server
```bash
python manage.py runserver
```

---

## Testing URLs
| URL | Expected Result |
|-----|-----------------|
| `http://127.0.0.1:8000/students/` | List of all students |
| `http://127.0.0.1:8000/students/1/` | John's details |
| `http://127.0.0.1:8000/students/2/` | Alice's details |
| `http://127.0.0.1:8000/students/999/` | 404 Not Found page |
| `http://127.0.0.1:8000/students/add/` | Add student form |

---

## Complete Flow Diagram
```
User clicks "View Details" for Alice
        ↓
{% url 'student_detail' student.id %}
        ↓
student.id = 2
        ↓
URL generated: /students/2/
        ↓
Django matches pattern: students/<int:id>/
        ↓
View receives: id=2
        ↓
get_object_or_404(Student, id=2)
        ↓
Alice found in database
        ↓
Template renders student details
        ↓
User sees Alice's information
```

---

## Key Django Features Used
| Feature | Purpose |
|---------|---------|
| `{% url %}` | Generate dynamic URLs by name |
| `get_object_or_404()` | Safely retrieve object or return 404 |
| `path("<int:id>/")` | Capture integer from URL |
| `render()` | Render template with context |
| `Student.objects.all()` | Get all students for list |
| `{% for %}` | Loop through students in list |