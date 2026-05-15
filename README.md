# Cats API 🐱

# 📌 Overview

The Cats API is a simple RESTful web service built using Django and Django REST Framework (DRF). The project demonstrates how to create a fully functional CRUD (Create, Read, Update, Delete) API for managing cat records.

---

# 🚀 Features

✅ Full CRUD API for Cats  
✅ Django REST Framework ViewSets  
✅ Automatic URL routing with DRF Routers  
✅ JSON serialization  
✅ Django Admin Panel  
✅ Browsable REST API  
✅ SQLite database support  

---

# 🛠 Technologies Used

- Python
- Django
- Django REST Framework (DRF)
- SQLite

---

# 📁 Project Structure

```text
Cats_API/
│
├── cat_project/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   ├── wsgi.py
│
├── cats/
│   ├── migrations/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   ├── admin.py
│   └── apps.py
│
├── venv/
├── manage.py
└── README.md
```

---

# ⚙️ Installation

## 1️⃣ Clone the Repository

```bash
git clone https://github.com/Tania1011/cats_api.git
cd cats-api
```

---

## 2️⃣ Create Virtual Environment

### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

### Mac/Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## 3️⃣ Install Dependencies

```bash
pip install django djangorestframework
```

---

# 🗄 Apply Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

---

# ▶️ Run the Development Server

```bash
python manage.py runserver
```

Open in browser:

```text
http://127.0.0.1:8000/
```


---

# 🐱 Cat Model

```python

class Cat(models.Model):
    name = models.CharField(max_length=100)
    kind = models.CharField(max_length=100)
    age = models.IntegerField()
    weight = models.FloatField()
    vaccinated = models.BooleanField(default=False)
```
---

# 🔄 Class Serializer

```python

class CatSerializer(serializers.ModelSerializer):

    class Meta:
        model = Cat
        fields = '__all__'
```

---


# 🌐 ViewSet

```python
from rest_framework import viewsets
from .models import Cat
from .serializers import CatSerializer

class CatViewSet(viewsets.ModelViewSet):
    queryset = Cat.objects.all()
    serializer_class = CatSerializer
```
---

# 🔧 Installed Apps

```python
INSTALLED_APPS = [

    'rest_framework',
    'cats',
]
```

---

# 🔗 URLs

## cats/urls.py

```python
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from .views import CatViewSet

router = DefaultRouter()
router.register(r'cats', CatViewSet)

urlpatterns = [
    path('', include(router.urls)),
]
```

---

## cat_project/urls.py

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('cats.urls')),
]
```

---


# 📡 API Endpoints

Base URL:

```text
http://127.0.0.1:8000/api/
```

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/cats/` | List all cats |
| POST | `/api/cats/` | Create a new cat |
| GET | `/api/cats/<id>/` | Retrieve one cat |
| PUT | `/api/cats/<id>/` | Update entire cat |
| PATCH | `/api/cats/<id>/` | Partial update |
| DELETE | `/api/cats/<id>/` | Delete a cat |

---

# 🧪 Example Requests

## Create a Single Cat

### POST `/api/cats/`

```json
{
    "name": "Lulu",
    "kind": "Scottish",
    "age": 3,
    "weight": 2.5,
    "vaccinated": false
}
```

---

## Example Response

```json
{
    "id": 2,
    "name": "Lulu",
    "kind": "Scottish",
    "age": 3,
    "weight": 2.5,
    "vaccinated": false
}
```

---

