---
layout: post
title:  "Como realizar integração de um projeto Django com o Github"
date:   2017-06-17
categories: tutorial
---

#### Autores:
* André Spadetto Leão
* Gabriel Bianchi
* Gabriel Barbosa

# Tutorial: Como realizar integração de um projeto Django com o GitHub
 
Este tutorial tem como objetivo explicar o que é necessário configurar em um projeto Django para possibilitar a realização do login no sistema, utilizando a api do Github. Na primeira seção serão apresentados os pré-requisitos, na segunda será mostrado como configurar um projeto Django simples e na terceira será apresentado um exemplo simples de como realizar o login e criar um repositório no Github.
 
Todos os exemplos deste tutorial serão feitos em um ambiente Linux com editor de texto Sublime Text e a versão do python a ser utilizada será a 3.5.
 
## 1 - Pré-requisitos
 
Para a configuração básica de um projeto Django, que realize a integração com o Github, serão necessários:
 
* Python >= 2.7
* Django >= 1.10
* social-auth-app-django 
* virtualenv
 
## 2 - Configuração de um projeto básico Django
### Ambiente Virtual
 
O virtualenv é um ambiente virtual muito utilizado no desenvolvimento de aplicações na linguagem Python. Cada aplicação pode utilizar um conjunto de ferramentas diferente, sendo assim o virtualenv cria um ambiente fazendo com que a aplicação trabalhe de forma isolada.
 
Para configura-lo é nescessário ter o Python instalado. Para instalá-lo abra um terminal e execute o comando: 
 
    sudo apt-get install virtualenv
  
Após a instalação, crie uma pasta onde o projeto será salvo com o comando:
 
    mkdir tutorial-django && cd tutorial-django
 
Para criar o ambiente basta entrar na pasta criada acima e executar o comando, no terminal:
 
    virtualenv -p python3 <nome_do_ambiente>
 
Neste tutorial, o nome_do_ambiente será "env". Para ativá-lo execute o comando:
 
    source env/bin/activate
 
Aparecerá a seguinte linha:
 
    (env)
 
Isso significa que seu ambiente virtual foi ativado e está pronto para ser utilizado.
 
Em seguida, para instalar o django e os módulos do exemplo, execute o comando:
 
    pip install django
 
### Criação e configuração do Projeto    
 
Para criar o projeto, em Django, entre na pasta "tutorial-django" e execute o comando:
 
    django-admin startproject <nome_projeto>
 
O nome_projeto, neste caso, será "project".
 
O comando *django-admin* é um script utilizado na a execução de tarefas administrativas como criação de projetos e modulos. 
 
Este comando cria a estrutura do projeto que ficará igual ao trecho de código abaixo:
 
    project
    ├───manage.py
    └───project
            settings.py
            urls.py
            wsgi.py
            __init__.py
 
O arquivo *manage.py*, assim como o comando *django-admin*, é um script que cuida da execução de tarefas administrativas. Além disso ele coloca o pacote do seu projeto no *sys.path* e aponta a variável de ambiente **DJANGO_SETTINGS_MODULE** para o arquivo *settings.py*.  A partir da criação do projeto, este comando será utilizado para a maioria das tarefas.
 
O arquivo *settings.py* é o local onde serão feitas as configurações do seu projeto. Abra o mesmo com o editor **Sublime Text**.   
 
Em **Internationalization** altere as seguintes linhas:
 
    LANGUAGE_CODE = 'pt-br'
    TIME_ZONE = 'America/Sao_Paulo'

O arquivo *urls.py* contém o resolvedor de padrões para as urls a serem utilizadas. No momento da configuração deste arquivo este conceito será melhor explicado.
 
O arquivo *wsgi.py* é o script que fará o deploy do projeto. O WSGI é a plataforma padrão de deploy de aplicações do Django.
 
Para rodar um projeto, você deve entrar na pasta onde o arquivo **manage.py** está localizado e executar o comando:
 
    python3 manage.py runserver
 
 
Para que o seu projeto fique bem estruturado, o Django possui um recurso chamado **app** que te permite modularizar o seu projeto. Assim o seu código ficará sempre organizado, facilitando sua leitura e eventuais manutenções.
 
Para criar um app entre na pasta onde o arquivo **manage.py** está e execute o comando:
 
    python3 manage.py startapp <nome_do_app> 
 
No lugar de nome_do_app coloque **app**.
 
Será criada a seguinte estrutura:
 
    app
    ├── admin.py
    ├── apps.py
    ├── __init__.py
    ├── migrations
    │   └── __init__.py
    ├── models.py
    ├── tests.py
    └── views.py
 
 
No arquivo *settings.py*, que se encontra dentro da pasta project, na opção 
*INSTALLED_APPS*, adicione ao final da linha o app criado, não esquecendo de adicionar a vírgula no final.
 
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app',
    ]
 
Antes de finalizar, faça o seguinte teste para ter certeza que seu banco de dados foi configurado corretamente. Execute o seguinte comando:
 
    python manage.py migrate
 
Este comando criará as tabelas principais do django para a continuação do projeto. Caso tudo esteja ok você receberá o seguinte retorno:
 
    Operations to perform:
      Apply all migrations: admin, contenttypes, auth, sessions
    Running migrations:
      Rendering model states... DONE
      Applying contenttypes.0001_initial... OK
      Applying auth.0001_initial... OK
      Applying admin.0001_initial... OK
      Applying admin.0002_logentry_remove_auto_add... OK
      Applying contenttypes.0002_remove_content_type_name... OK
      Applying auth.0002_alter_permission_name_max_length... OK
      Applying auth.0003_alter_user_email_max_length... OK
      Applying auth.0004_alter_user_username_opts... OK
      Applying auth.0005_alter_user_last_login_null... OK
      Applying auth.0006_require_contenttypes_0002... OK
      Applying auth.0007_alter_validators_add_error_messages... OK
      Applying sessions.0001_initial... OK
    (env)
 
Com as explicações feitas sobre a estrutura e os comandos do django, tem-se uma base para realizar a criação de qualquer projeto em django. 

## 3 - Exemplo login com o Github
 
Para fazer a autenticação com o GitHub, utilizaremos a biblioteca social-auth-app-django. Além de prover a autenticação com o GitHub ela fornece o serviço de autenticação com o Facebook, Twitter, entre outros.
 
Utilize o projeto anterior com base para as próximas configurações e realize a instalação da biblioteca com o seguinte comando:
  
    pip install social-auth-app-django
 
Em seguida abra o arquivo **settings.py** , vá até a linha **INSTALLED_APPS** e insira a linha  'social_django':
 
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app',
        'social_django',  
    ]
 
Execute o comando:
 
    python3 manage.py migrate
 
Agora vá até **MIDDLEWARE_CLASSES** a adicione a seguinte linha:
 
    MIDDLEWARE_CLASSES = [
        'django.middleware.security.SecurityMiddleware',
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.middleware.common.CommonMiddleware',
        'django.middleware.csrf.CsrfViewMiddleware',
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        'django.contrib.auth.middleware.SessionAuthenticationMiddleware',
        'django.contrib.messages.middleware.MessageMiddleware',
        'django.middleware.clickjacking.XFrameOptionsMiddleware',
   
        'social_django.middleware.SocialAuthExceptionMiddleware',  # <--
    ]
 
Em **TEMPLATES** adicione as seguinte linhas:
 
    TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [
             PROJECT_DIR.child('templates'),
         ],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
   
                'social_django.context_processors.backends',  # <--
                'social_django.context_processors.login_redirect', # <--
            ]
        },
    },
    ]
 
Adicione o código abaixo no final do arquivo:
 
    AUTHENTICATION_BACKENDS = (
        'social_core.backends.github.GithubOAuth2',
        'django.contrib.auth.backends.ModelBackend',
     ) 
 
Salve as alterações.
 
Para realizar a comunicação com a API do Github é necessário gerar um token de autorização. Para isso, acesse o link:
 
   [https://github.com/settings/applications/new](https://github.com/settings/applications/new)
 
Em authorization call back URL coloque a seguinte url:
 
    http://localhost:8000/oauth/complete/github
 
Caso sua aplicação esteja hospedada em algum servidor, substitua **localhost:8000** pelo endereço da mesma.
 
Agora vá até o arquivo **settings.py** e adicione a seguinte linhas no final do arquivo:
 
    SOCIAL_AUTH_GITHUB_KEY = <client_id>
    SOCIAL_AUTH_GITHUB_SECRET = <client_secret>
 
O valor de **client_id** e **client_secret** devem estar entre aspas simples. Exemplo:
  
    SOCIAL_AUTH_GITHUB_KEY = '44fd4145a8d85fda4ff1'
 
Para poder dar permissão para a criação do repositório, é necessário que o usuário authorize ao logar. Para isso, é necessário que o escopo do projeto peça ao usuário esse tipo de autorização. Adicione as seguintes linhas ao final do arquivo **settings.py**
 
    SOCIAL_AUTH_GITHUB_SCOPE = [
        'user',
        'read:org',
        'public_repo',
        'admin:repo_hook',
        'admin:org',
        'user:email'
    ]
 
Vá até o arquivo **urls.py** e adicione as seguintes linhas:
  
    from django.conf.urls import url, include
    from django.contrib import admin
    from django.contrib.auth import views as auth_views
   
    from app.views import *
   
    urlpatterns = [
        url(r'^$', home, name='home'),
        url(r'^login/$', auth_views.login, name='login'),
        url(r'^logout/$', auth_views.logout, name='logout'),
        url(r'^oauth/', include('social_django.urls', namespace='social')),  # <--
        url(r'^admin/', admin.site.urls),
    ]
 
Agora adicione as seguintes linhas no arquivo **settings.py**:
 
    LOGIN_URL = 'login'
    LOGOUT_URL = 'logout'
    LOGIN_REDIRECT_URL = 'home'
 
Dentro da pasta **app** crie uma pasta chamada **templates**:
 
    app
    ├── admin.py
    ├── apps.py
    ├── __init__.py
    ├── migrations
    │   └── __init__.py
    ├── models.py
    ├── templates  <---
    ├── tests.py
    └── views.py
 
Esta pasta é responsável por conter as páginas html do projeto. 
 
Crie um arquivo com o nome **base.html** e adicione o seguinte conteúdo:
    
    {% raw %}
    {% load staticfiles %}
    <!DOCTYPE html>
    <html>
    <head>
        <title>Trabalho LES</title>
    </head>
     <body>
        {%block content%}
        {% endblock %}
    </body>
    </html>
    {% endraw %}
 
 
Em seguida crie o arquivo **home.html** com o seguinte conteúdo:
 
    {% raw %}
    {% extends 'base.html' %}

    {% block content %}
         <p>Bem-vindo {{ user.username }}!</p>

    {% endblock %}
    {% endraw %}
 
Por fim, crie a view **home** no arquivo **views.py**:
 
    from django.contrib.auth.decorators import login_required
    from django.shortcuts import render
   
    @login_required
    def home(request):
        return render(request, 'templates/home.html')
 
Essas são as configurações básicas da biblioteca. Em seguida será mostrado um exemplo, de como fazer uma autenticação e criação de um repositório.
 
Para a autenticação com o github, na da pasta templates crie uma pasta com o nome **registration** e em seguida crie o arquivo **login.html** dentro desta com o seguinte conteúdo:
  
    {% raw %}
    {% extends 'base.html' %}
     
    {% block content %}
        <h2>Login</h2>
        <a href="{% url 'social:begin' 'github' %}">Login with GitHub</a><br>
    {% endblock %}
    {% endraw %}
 
Pronto. Para testar se tudo está funcionando corretamente, vá até a pasta onde se encontra o arquivo **settings.py** pelo terminal e digite o comando:
 
    python3 manage.py runserver
 
Entre no navegador e digite **localhost:8000** e tente realizar o login clicando no botão. Se tudo der certo, você será redirecionado para a página principal onde será exibido uma mensagem de boas vindas e as opções de criação de um repositório.
 
Para testar a funcionalidade de criar um repositório no Github criamos um formulário onde o usuário digitará o nome do repositório e a linguagem do gitignore. Crie um arquivo dentro da pasta **app** com o nome **forms.py** e insira as seguintes linhas:
    {% raw %}
    from django import forms
   
    class formRepositorio(forms.Form):
        nome = forms.CharField(label='Nome do repositório:', max_length=100)
        linguagem = forms.CharField(label='Linguagem:', max_length=100)
    {% endraw %}
Em seguida cria um arquivo com o nome **repositorio.html** na pasta templates com o seguinte conteúdo:
  
    {% raw %}
    {% extends 'base.html' %}
     
    {% block content %}
        <form method="post" action="{% url 'criar_repositorio' %}">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit">Criar</button>
         </form>
    {% endblock %}
    {% endraw %}
 
Agora crie a view e o método a seguir  no arquivo **views.py**:
 
    import requests 
    from django.shortcuts import redirect
    from .forms import *
   
    def cria_repositorio_github(token, nome, linguagem):
        r = requests.post('http://localhost:8001/cria_repositorio/', data={'nome_repositorio':nome, 'token':token, 'linguagem':linguagem})
   
    @login_required
    def criar_repositorio(request):
        if request.method == 'POST':
            form = formRepositorio(request.POST)
            if form.is_valid():
                user = request.user
                token = user.social_auth.get(provider='github').access_token
                nome_repositorio = form.cleaned_data['nome']
                linguagem = form.cleaned_data['linguagem']
                r = cria_repositorio_github(token, nome_repositorio, linguagem)
                return redirect('home')
        else:
            form = formRepositorio()
        return render(request, 'repositorio.html', {'form':form})
 
A view **criar_repositorio** recebe o que o usuário digitou na tela, e em seguida chama a função **cria_repositorio_github()** que realiza a comunicação com o micro serviço do github através de uma requisição POST. Este micro serviço foi desenvolvido previamente, utilizando a biblioteca **PyGithub**, e seu código poderá ser acessado neste [link](https://github.com/gabriellmb05/api-github-1). Para mais detalhes sobre quais métodos podem ser utilizados nesta biblioteca entre no [link](http://pygithub.readthedocs.io/en/latest/introduction.html). Ao logar com o github, a api social armazena o token de autorização do usuário logado no banco de dados. Dessa forma, quando for necessário realizar alguma comunicação com a api do Github, este poderá ser acessado como um atributo como pode ser visto na linha abaixo:
 
    token = user.social_auth.get(provider='github').access_token
 
Agora adicione a seguinte linha no arquivo **home.html**:
  
    {% raw %}  
    {% extends 'base.html' %}

    {% block content %}
         <p>Bem-vindo {{ user.username }}!</p>
         <a href="{% url 'criar_repositorio' %}">Criar repositório</a>  #<----
    {% endblock %}
    {% endraw %}
 
No arquivo **urls.py** adicione a seguinte linha:
 
    url(r'^criar_repositorio/$', core_views.criar_repositorio, name='criar_repositorio'),
 
Feito isso, o sistema estará pronto para realizar o login com o Github e criar um repositório com o nome escolhido e adicionando automaticamente um arquivo **.gitignore** com a linguagem escolhida. Execute o comando abaixo e realize os testes:
 
    python3 manage.py runserver
 
Lembre-se de que deve estar na pasta onde o arquivo **manage.py** se encontra antes de executar o comando.
 
Todo o código implementado deste tutorial encontra-se no
[link](https://github.com/asleao/tutorial-github).


## Referências
 
[How to Add Social Login to Django](https://simpleisbetterthancomplex.com/tutorial/2016/10/24/how-to-add-social-login-to-django.html)
[Documentacao do Django](https://www.djangoproject.com/start/)
