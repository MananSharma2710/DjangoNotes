## Structure of Django Project

```
project_name/       // Outer Project Folder/Root Directory
|
|
├── project_name/   //Inner Project folder
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
|
|
|
├── manage.py

```

1. `__init__.py` : 
    - The folder which contains __init__.py file is considered as python package.
    - It can be an empty file or include initialization code if needed.

2. `wsgi.py` :
    -  WSGI (Web Server Gateway Interface) is a specification that describes how a web server communicates with web applications, and how web applications can be chained together to process one request.
    - It provides a standard for synchronous Python apps.
    -  It provides a bridge between the application and the web server, allowing them to communicate effectively.

3. `asgi.py` :
    - ASGI (Asynchronous Server Gateway Interface) is a spiritual successor to WSGI, intended to provide a standard interface between async-capable Python web servers, frameworks, and applications.
    - This file is used for serving the application asynchronously, making it suitable for deployment with asynchronous servers like Daphne or Uvicorn.
    - It has become more important with the rise of asynchronous programming in web applications.
    - It provides standards for both asynchronous and synchronous apps.

4. `settings.py` : 
    - This file contains various settings for our Django project.
    - It includes configuration options such as database settings, installed apps, middleware, authentication settings, and more.
    - This is where we configure the behavior of our project.

5. `urls.py` :
    - This file is responsible for URL routing within our project.
    - It defines the mapping between URLs and views (or viewsets in the case of DRF) for the project.
    - Each app can also have its own urls.py to handle its specific URLs.

6. `manage.py` : 
    - It is automatically created in each Django project
    - A command-line utility for interacting with the project.
    - It sets the DJANGO_SETTINGS_MODULE environment variable so that it points to our project's setting.py file.
    - We can use it to run development server, manage database migrations, and perform other tasks.
    - Generally, when working on a single Django project, it's easier to use manage.py than django-admin.

7. `project_name/` : 
    - This is the main project package. 
    - The inner `project_name` directory contains settings for the project, URL routing, and ASGI configuration for deployment. `settings.py` contains project settings like database configuration, installed apps, middleware, etc.

