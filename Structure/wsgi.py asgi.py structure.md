## STRUCTURE of wsgi.py 

```python
import os
from django.core.wsgi import get_wsgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'project_name.settings')
application = get_wsgi_application()
```

* `import`: 
    + This keyword is used to bring modules or packages into your Python code, making their functionality available for use.

* `os`: 
    + This is the Python module that provides functions for interacting with the operating system. 
    + It allows us to access various OS-related features, including environment variables and file operations.

* `from`:
    + This keyword is used along with the `import` keyword to specify the module or specific parts of the module you want to import.

* `django.core.wsgi`:
    + This is the module within the Django framework that handles the Web Server Gateway Interface (WSGI) integration for Django applications.

* `import get_wsgi_application`:
    + This imports the `get_wsgi_application` function from the `django.core.wsgi` module.
    + This function is used to get the WSGI application object that represents our Django application.

* `os.environ`:
    + A mapping object representing the string environment.
    + This accesses the environment variables in the operating system.
    + It's a dictionary-like object that stores environment variables and their values. 

* `setdefault`:
    + This is a method that sets a default value for a dictionary key if the key does not already exist in the dictionary.

* `'DJANGO_SETTINGS_MODULE'`:
    + This is an environment variable used by Django to determine which settings module to use for the project.

* `'project_name.settings'`:
    + This is the value that the `'DJANGO_SETTINGS_MODULE'` environment variable is being set to.
    + Replace `'project_name'` with the actual name of our Django project.

* `application`:
    + This is a variable name chosen to store the WSGI application object that will be returned by the `get_wsgi_application()` function.

* `get_wsgi_application()`:
    + This is a function call that retrieves the WSGI application object.
    + This object is an instance of a class that implements the WSGI specification, allowing it to communicate with WSGI-compatible web servers.

So, the `wsgi.py` file's purpose is to set up the necessary environment variable for Django's settings module and to retrieve the WSGI application object, which is used to serve your Django application on a WSGI-compatible web server.



```
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'project_name.settings')
```

- When the WSGI server loads our application. Django needs to import the settings module, that's where our entire application is defined.

- Django uses the DJANGO_SETTINGS_MODULE environment variable to locate the appropriate settings module.

- It must contain the dotted oath to the settings module.

- We can use a different value for developmet and production, it all depends on how we organize our settings.

- If this variable isn't set, the default wsgi.py sets it to *`project_name.settings`*, where `'project_name'` is the actual name of our Django project.

- That's how runserver discovers the default settings file by default.



## STRUCTURE of asgi.py

```python
import os
from django.core.asgi import get_asgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'project_name.settings')
application = get_asgi_application()
```


- `django.core.asgi`:
    + This is the module within the Django framework that handles the Asynchronous Server Gateway Interface (ASGI) integration for Django applications.

- `import get_asgi_application`:
    + This imports the `get_asgi_application` function from the `django.core.asgi` module.
    + This function is used to get the ASGI application object that represents your Django application in an asynchronous context.

- `get_asgi_application()`:
    + This is a function call that retrieves the ASGI application object.
    + This object is an instance of a class that implements the ASGI specification, allowing it to communicate with ASGI-compatible servers in an asynchronous manner.

So, the `asgi.py` file's purpose is to set up the necessary environment variable for Django's settings module and to retrieve the ASGI application object, which is used to serve your Django application on ASGI-compatible asynchronous web servers.