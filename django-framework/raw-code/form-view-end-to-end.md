# Add Student Form - Complete Implementation

## File Structure

```
myproject/
├── myproject/
│   └── urls.py           # ← Include the app's URLs here
├── myapp/
│   ├── templates/
│   │   └── myapp/
│   │       └── student_form.html
│   ├── urls.py           # ← Your new URL config
│   └── views.py          # ← Your new view
└── manage.py
```

---

## 1. Template File
**`myapp/templates/myapp/student_form.html`**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Add Student</title>
</head>
<body>

    <h1>Add Student</h1>

    <form>

        <p>
            <label>Name</label><br>
            <input type="text" name="name">
        </p>

        <p>
            <label>Email</label><br>
            <input type="email" name="email">
        </p>

        <p>
            <label>Age</label><br>
            <input type="number" name="age">
        </p>

        <button type="submit">
            Save
        </button>

    </form>

</body>
</html>
```

---

## 2. Views
**`myapp/views.py`**
```python
from django.shortcuts import render

def student_create(request):
    return render(request, "myapp/student_form.html")
```

---

## 3. App URLs
**`myapp/urls.py`**
```python
from django.urls import path
from . import views

urlpatterns = [
    path("students/add/", views.student_create, name="student_create"),
]
```

---

## 4. Project URLs
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

## 5. Run Server
```bash
python manage.py runserver
```

---

## 6. Access the Page
```
http://127.0.0.1:8000/students/add/
```