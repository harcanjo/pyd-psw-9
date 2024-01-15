# Notas do material de apoio

## Configurações iniciais

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

## Inicio da tela de Cadastro no app de usuarios

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

At usuarios/views.py

```py
def cadastro(request):
 if request.method == 'GET':
  return render(request, 'cadastro.html')
```

At study_async/settings.py

```py
import os
...
TEMPLATES = [
  {
    ...
    'DIRS':[os.path.join(BASE_DIR, 'templates')],
    ...
  }
]
```

At templates/base.html

```html
{% load static %}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
    <title>Study Async</title>
    {% block 'cabecalho' %} {% endblock %}
  </head>
  <body>
    {% block 'conteudo' %}{% endblock %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

At usuarios/templates/base.html

```html
{% extends 'base.html' %} {% block 'conteudo' %}
<div class="bg1">
  <div class="container">
    <div class="row">
      <div class="col-md">
        <div class="box-titulo">
          <div class="box-titulo-item">
            <img src="" />
          </div>
          <div
            style="margin-top: auto; margin-bottom: auto;"
            class="box-titulo-item"
          >
            <h3>Study.Async</h3>
          </div>
        </div>
        <hr class="divisor" />
        <br />
        <div class="tac">
          <h4 style="font-size: 30px">
            Sua plataforma online<br />
            para te ajudar nos estudos
          </h4>
        </div>
      </div>
      <div class="col-md">
        <br />
        <br />
        <div class="box-form">
          <div class="box-circle">
            <div class="circle c1"></div>
            <div class="circle c2"></div>
            <div class="circle c3"></div>
          </div>
          <br />
          <h3>Cadastre-se</h3>
          <form action="" method="POST">
            <label>Username</label>
            <input type="text" class="input-form" name="username" id="" />
            <br />
            <br />
            <label>Senha</label>
            <input type="password" class="input-form" name="senha" id="" />
            <br />
            <br />
            <label>Confirmar senha</label>
            <input
              type="password"
              class="input-form"
              name="confirmar_senha"
              id=""
            />
            <br />
            <br />
            <input type="submit" value="Enviar" class="btn-cadastro" />
            <br />
            <br />
            <br />
            <br />
          </form>
        </div>
      </div>
    </div>
  </div>
</div>
{% endblock 'conteudo' %}
```

At study_async/settings.py

```py
STATIC_URL = '/static/'
STATICFILES_DIRS = (os.path.join(BASE_DIR, 'templates/static'),)
STATIC_ROOT = os.path.join('static')
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

```css
:root {
  --main-color: #0b1526;
  --dark-color: #000716;
  --secondary-dark-color: rgb(15, 2, 26);
  --light-color: #00c1f3;
  --contrast-color: #f4c96b;
  --differential-color: #58fcd5;
}

body {
  background-color: var(--dark-color) !important;
  color: white !important;
}
```

No arquivo templates/base.html importe o arquivo css:

```css
<link href="{% static 'geral/css/base.css' %}" rel="stylesheet">
```

Crie o arquivo templates/static/usuarios/css/cadastro.css

```css
* {
  margin: 0;
  padding: 0;
}

.bg1 {
  background-image: url("/static/usuarios/img/bg1.png") !important;
  height: 100vh;
  background-size: cover;
}

.titulo-fonte {
  margin-top: 20px;
}

.box-titulo {
  display: flex;
}

.divisor {
  border: 0;
  height: 1px;
  background-image: linear-gradient(
    to right,
    transparent,
    rgb(162, 219, 236),
    transparent
  );
  display: block;
}

.tac {
  text-align: center;
}

.box-form {
  padding: 20px;
  background-color: rgba(217, 217, 217, 0.05);
  color: white !important;
}

.box-circle {
  display: flex;
  gap: 5px;
}

.circle {
  width: 16px;
  height: 16px;
  border-radius: 8px;
}

.c1 {
  background-color: #3e79eb;
}

.c2 {
  background-color: #29bfc9;
}

.c3 {
  background-color: #d98562;
}

.input-form {
  background-color: #0b1526;
  padding: 10px;
  border: none;
  border: 1px solid rgba(88, 252, 213, 0.4);
  color: white;
  outline: 0;
  width: 100%;
}

.btn-cadastro {
  padding: 10px;
  background-color: #58fcd5;
  border: none;
  border: 1px solid #58fcd5;
  font-size: 18px;
  font-weight: bold;
  padding-left: 25px;
  padding-right: 25px;
}
```

Importe o arquivo css em cadastro.html:

```css
{% load static %}

{% block 'cabecalho' %}
    <link href="{% static 'usuarios/css/cadastro.css' %}" rel="stylesheet">
{% endblock %}
```

Adicione o bg1.png e o logo.png na pasta /templates/static/usuarios/img
Adicione a logo em cadastro.html:

```html
<img src="{% static 'usuarios/img/logo.png' %}" />
```

Execute as migrações:

```bash
python manage.py makemigrations
python manage.py migrate
```

Prepare o form para enviar os dados para a View:

```html
<form action="{% url 'cadastro' %}" method="POST">{% csrf_token %}</form>
```

Na view cadastro:

```py
def cadastro(request):
    if request.method == 'GET':
        return render(request, 'cadastro.html')
    else:
        username = request.POST.get('username')
        senha = request.POST.get('senha')
        confirmar_senha = request.POST.get('confirmar_senha')

        if not senha == confirmar_senha:
            return redirect('/usuarios/cadastro')

        user = User.objects.filter(username=username)

        if user.exists():
            return redirect('/usuarios/cadastro')

        try:
            user = User.objects.create_user(
                username=username,
                password=confirmar_senha,
            )

            return redirect('/usuarios/login')
        except:

            return redirect('/usuarios/cadastro')
```

Configure as mensagens

```py
from django.contrib.messages import constants

MESSAGE_TAGS = {
    constants.DEBUG: 'alert-primary',
    constants.ERROR: 'alert-danger',
    constants.SUCCESS: 'alert-success',
    constants.INFO: 'alert-info',
    constants.WARNING: 'alert-warning',
}
```

Adicione as mensagens em pontos específicos de sua View:

```py
def cadastro(request):
    if request.method == 'GET':
        return render(request, 'cadastro.html')
    else:
        username = request.POST.get('username')
        senha = request.POST.get('senha')
        confirmar_senha = request.POST.get('confirmar_senha')

        if not senha == confirmar_senha:
            messages.add_message(
                request, constants.ERROR, 'As senhas não coincídem'
            )
            return redirect('/usuarios/cadastro')

        user = User.objects.filter(username=username)

        if user.exists():
            messages.add_message(
                request,
                constants.ERROR,
                'Já existe um usuário com o mesmo username',
            )
            return redirect('/usuarios/cadastro')

        try:
            user = User.objects.create_user(
                username=username,
                password=confirmar_senha,
            )
            messages.add_message(
                request, constants.ERROR, 'Usuário cadastrado com sucesso.'
            )
            return redirect('/usuarios/login')
        except:
            messages.add_message(
                request, constants.ERROR, 'Erro interno do sistema'
            )
            return redirect('/usuarios/cadastro')
```

Exiba as mensagens:

```html
{% if messages %} {% for message in messages %}
<section class="alert {{message.tags}}">{{message}}</section>
{% endfor %} {% endif %}
```

## Fim da tela de Cadastro

---
