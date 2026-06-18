# Projeto Django — Guia de Implementação

---

## Antes de começar

Este guia vai te ajudar a transformar o protótipo HTML do seu grupo em uma aplicação Django funcional.

> Substitua `nome_do_app` pelo nome escolhido pelo grupo em todos os arquivos.

---

# Passo 0 — Criar o Projeto

## Criar ambiente virtual

```powershell
python -m venv venv
```

## Ativar ambiente virtual

```powershell
.\venv\Scripts\Activate.ps1
```

## Instalar Django

```powershell
pip install django
```

## Criar requirements.txt

```powershell
pip freeze > requirements.txt
```

## Criar projeto Django

```powershell
django-admin startproject config .
```

## Rodar servidor

```powershell
python manage.py runserver
```

---

## Passo 1 — Criar o App

```bash
python manage.py startapp nome_do_app
```

---

## Passo 2 — Ativar o App

Arquivo: `config/settings.py`

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'nome_do_app',  # ← adicione aqui
]
```

---

## Passo 3 — Configurar URLs do Projeto

Arquivo: `config/urls.py`

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("nome_do_app/", include("nome_do_app.urls")),
    path("admin/", admin.site.urls),
]
```

Agora teremos:

```
/nome_do_app/   -> seu projeto
/admin/         -> administração do Django
```

---

## Passo 4 — Criar o urls.py do App

Crie o arquivo:

`nome_do_app/urls.py`

```python
from django.urls import path
from . import views

app_name = "nome_do_app"

urlpatterns = [
    path("", views.tela1, name="tela1"),
    path("tela2/", views.tela2, name="tela2"),
    path("tela3/", views.tela3, name="tela3"),
]
```

> Substitua `tela1`, `tela2` e `tela3` pelos nomes que fazem sentido para o seu projeto.
> Exemplo: `index`, `sobre`, `contato` ou `inicio`, `atividades`, `equipe`.

---

## Passo 5 — Criar as Views

Arquivo: `nome_do_app/views.py`


```python
from django.shortcuts import render
from django.http import HttpResponse

def tela1(request):
    return HttpResponse("Tela 1")

def tela2(request):
    return HttpResponse("Tela 2")

def tela3(request):
    return HttpResponse("Tela 3")
```


```python
from django.shortcuts import render

def tela1(request):
    return render(request, "nome_do_app/tela1.html")

def tela2(request):
    return render(request, "nome_do_app/tela2.html")

def tela3(request):
    return render(request, "nome_do_app/tela3.html")
```

### Testar

```bash
python manage.py runserver
```

Acesse cada URL e verifique se o servidor responde sem erros antes de continuar.

---
