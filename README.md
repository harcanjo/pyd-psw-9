# PSW 9.0 - PYSTACKWEEK 9.0 | Pythonando

## Projeto StudyAsync

[Figma: StudyAsync](https://www.figma.com/file/lScIF34y6BVRbyp2g8c2Cl/Untitled?type=design&node-id=0%3A1&mode=design&t=QHCxV7YpFU6S853N-1)

## Config

```bash
python -m venv venv
python3 -m venv venv

venv\Script\activate
source venv/bin/activate

pip install django
pip install pillow
```

## Project created with

```bash
django-admin startproject study_async .

python manage.py runserver

python manage.py startapp usuarios
```

## Register

At stydy_async/urls.py

```py
path('usuarios/', include('usuarios.urls')),
```

At usuarios create a urls.py

```py
from django.urls import path
from . import views
urlpatterns = [
 path('cadastro/', views.cadastro, name='cadastro'),
]
```
