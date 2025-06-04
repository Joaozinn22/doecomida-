# ZeroFome - Aplicativo de Doação de Alimentos

O **ZeroFome** é um aplicativo que conecta pessoas com alimentos sobrando (como mercados ou indivíduos) a ONGs ou pessoas em situação de vulnerabilidade.  
Alinhado com o Objetivo de Desenvolvimento Sustentável: **Fome Zero e Agricultura Sustentável**.

---

## 👥 Equipe
- João Gabriel de Moraes Gonçalves

---

## 🚀 Funcionalidades Básicas
- Cadastro de usuários (doador e receptor)  
- Publicação de alimentos disponíveis  
- Solicitação de retirada  
- Histórico de doações

---

## 🧩 Histórias de Usuário

1. Como doador, quero me cadastrar no aplicativo para oferecer alimentos.  
2. Como receptor, quero me cadastrar no aplicativo para receber doações.  
3. Como doador, quero publicar os alimentos disponíveis com descrição e validade.  
4. Como receptor, quero visualizar uma lista de alimentos disponíveis perto de mim.  
5. Como receptor, quero solicitar a retirada de um alimento para garantir o recebimento.  
6. Como doador, quero visualizar as solicitações de retirada para decidir quem receberá.  
7. Como doador, quero marcar um alimento como doado para evitar duplicidade.  
8. Como receptor, quero acompanhar o status da minha solicitação (pendente, aceito, entregue).  
9. Como usuário, quero ver meu histórico de doações ou recebimentos para controle pessoal.  
10. Como administrador, quero poder moderar conteúdos inapropriados ou denúncias.

---

## 🗂️ Quadro de Tarefas (Trello)

![Print do Quadro](https://github.com/Joaozinn22/doecomida-/blob/main/Captura%20de%20tela%202025-05-27%20212151.png?raw=true)

---

## 🎨 Protótipos Lo-Fi

Veja os protótipos no Figma: [Acessar protótipos](https://www.figma.com/proto/1upDO2TPENuhnaBP44mQRU/Untitled?node-id=1-12&p=f&t=rzjg3G2TP3eF2CSP-0&scaling=scale-down&content-scaling=fixed&page-id=0%3A1)

---

## 🎥 Screencast

Apresentação em vídeo com protótipos e explicações: [Assista aqui](https://drive.google.com/drive/u/0/folders/1q4b6duI1pyHfOjFwyjVzonSlzR-h246D)

---

## Estrutura do Projeto e Códigos Principais

O projeto está organizado da seguinte forma dentro da pasta principal `apsapp`:

### Pasta principal: `apsapp/`

Contém os arquivos principais do projeto Django, como:

**Configurações (`settings.py`):**

```python
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = 'django-insecure-tk!$hqc8sdzr963xo*7z08*r4bu67*9#-^-b7l8r%dr)e8nyn!'

DEBUG = True

ALLOWED_HOSTS = []

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'sistema',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'apsapp.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'apsapp.wsgi.application'

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

AUTH_PASSWORD_VALIDATORS = [
    {'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',},
    {'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',},
    {'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',},
    {'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',},
]

LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'UTC'

USE_I18N = True

USE_TZ = True

STATIC_URL = 'static/'

DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

URLs gerais (urls.py):
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('sistema.urls')),
]

App principal: sistema/
Contém:

Modelos (models.py):
from django.db import models
from django.utils import timezone

class Perfil(models.Model):
    nome = models.CharField(max_length=100)
    email = models.EmailField()

class Alimento(models.Model):
    nome = models.CharField(max_length=100)
    descricao = models.TextField()
    data_publicacao = models.DateTimeField(default=timezone.now)

Views (views.py):

from django.shortcuts import render
from .models import Alimento

def lista_alimentos(request):
    alimentos = Alimento.objects.all()
    return render(request, 'sistema/lista_alimentos.html', {'alimentos': alimentos})

URLs específicas do app (urls.py):

from django.urls import path
from . import views

urlpatterns = [
    path('alimentos/', views.lista_alimentos, name='lista_alimentos'),
]

Admin (admin.py):

from django.contrib import admin
from .models import Alimento, Perfil

admin.site.register(Alimento)
admin.site.register(Perfil)


