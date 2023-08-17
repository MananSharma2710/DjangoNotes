## STRUCTURE of settings.py

```python
import os
```

- `import`:
    + This keyword is used to bring modules or packages into our Python code, making their functionality available for use.

- `os`:
    + This is the Python module that provides functions for interacting with the operating system.
    + It allows us to access various OS-related features, including environment variables and file operations.

```python
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
```

- `BASE_DIR`:
    + This is a variable used to store the base directory of our Django project.
    + It's calculated by getting the absolute path of the directory containing the current `settings.py` file.

```python
SECRET_KEY = 'your_secret_key_here'
```

- `SECRET_KEY`:
    + It is used to provide cryptographic signing, and should be set to a unique, unpredictable value.
    + *django-admin startproject* automatically adds a randomly-generated `SECRET_KEY` to each new project.
    + This is a unique, secret string used to provide security in our Django application.
    + Django will refuse to start if `SECRET_KEY` is not set.
    + Replace `'your_secret_key_here'` with a strong and confidential secret key.

### Uses
+ All sessions if we are using any other session backend than *django.contrib.sessions.backends.cahce*, or are using the default *get_session_auth_hash()*.

+ All messgaes if we are using CookieStorage or FallbackStorage.

+ All PasswordResetView tokens.

+ Any usage of cryptographic signing, unless a different key is provided.


```python
DEBUG = True
```

- `DEBUG`:
    + This setting controls whether the application is in "debug" mode or not.
    + In debug mode, Django will display detailed error pages and additional debugging information.
    + In production, it's recommended to set this to `False`.
    + If DEBUG if *False*, we also need to properly set the `ALLOWED_HOSTS` setting.
    + Failing to do so will result in all requests being returned as "Bad Request (400)".


```python
ALLOWED_HOSTS = []
```

- `ALLOWED_HOSTS`:
    + This is a list of host/domain names that are allowed to access our Django application.
    + Values in this list can be fully qualified names (e.g. 'www.example.com'), in which case they will be matched against the request's Host header exactly (case-insensitive, not including port).
    + A value beginning with a period can be used as a subdomain wildcard: '.example.com' will match example.com, www.example.com and any other subdomain of example.com.
    + A value of '*' will match anything; in this case we are responsible to provide our own validation of the Host header.
    + In production, you should specify the actual domain names or IP addresses that your application will be hosted on.


```python
INSTALLED_APPS = [
    #Built-in Applications...
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

- `INSTALLED_APPS`:
    + This is a list of all installed applications in our Django project.
    + Each string should be a dotted Python path to an application configuration class (preferred) or a package containg an application.
    + An "application" in Django is a module designed to be reused in various projects.
    + Application names and labels must be unique in INSTALLED_APPS.
    + Application names- The dotted Python path to the appplication package must be unique. There is no way to include the same application twice, short of duplicating its code under another name.
    + Application labels- By default the final part of the name must be unique too. For example, you can't include both django.contrib.auth and myproject.auth


```python
MIDDLEWARE = [
    # ...
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```

- `MIDDLEWARE`:
    + This is a list of middleware classes that process requests and responses in your Django application. 
    + Middleware can perform various functions, such as authentication, security, and modifying the request/response.


```python
ROOT_URLCONF = 'project_name.urls'
```

- `ROOT_URLCONF`:
    + A string representing the full Python import path our root URLconf, for example `mydjangoapps.url` can be overridden on a per-request basis by setting the attribute urlconf on the incoming HttpRequest object.
    + This setting points to the URL configuration module for our project.
    + Replace `'project_name.urls'` with the actual path to our project's `urls.py` file.


```python
TEMPLATES = [
    # ...
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

- `TEMPLATES`:
    + This is a list of template engines and their configurations.
    + Templates are used to generate HTML dynamically in your views.
    + Each item of the list is a dictionary conatining the options for an individual engine.

- `'BACKEND': 'django.template.backends.django.DjangoTemplates'`:
    + This line specifies the backend template engine to be used, which is the built-in Django template engine.

- `'DIRS': []`:
    + This line specifies a list of additional template directories where Django should look for template files. + In this example, the list is empty, meaning that templates will be looked up only within the app directories and the built-in Django templates.

- `'APP_DIRS': True`:
    + This line indicates that Django should also search for templates within the `templates` subdirectory of each installed app.
    + This is set to `True`, which is the default behavior.

- `'OPTIONS': { ... }`:
    + This line introduces a nested dictionary that holds additional options for the template engine configuration.

- `'context_processors': [ ... ]`:
    + This line specifies a list of context processors that will be applied to every template rendering.
    + Context processors are functions that provide additional context variables to every template.

- `'django.template.context_processors.debug'`:
    + This context processor adds a `debug` variable to the template context, indicating whether the application is in debug mode.

- `'django.template.context_processors.request'`:
    + This context processor adds the `request` variable to the template context, giving access to the current request object.

- `'django.contrib.auth.context_processors.auth'`: 
    + This context processor adds the `user` and `perms` variables to the template context, providing information about the currently logged-in user and their permissions.

- `'django.contrib.messages.context_processors.messages'`:
    + This context processor adds the `messages` variable to the template context, providing access to messages that need to be displayed to the user.


```python
WSGI_APPLICATION = 'project_name.wsgi.application'
```

- `WSGI_APPLICATION`:
    + This setting points to the WSGI application object for our project.
    + The full Python path of the WSGI application object that Django's built-in servers (e.g. runserver) will use.
    + The *django-admin startproject* management command will create a standard `wsgi.py` file with an application callable in it, and point this setting to that application.
    + If not set, the return value of `django.core.wsgi.get_wsgi_application()` will be used.
    + Replace `'project_name.wsgi.application'` with the actual path to your project's `wsgi.py` file.


```python
DATABASES = {
    'default': {
        # ...
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```

- `DATABASES`:
    + This dictionary holds the database configuration for our project.
    + We specify the database engine, name, user, password, and other settings here.
    + It is a nested dictionary whose contents map a database alias to a dictionary conatinaing the options for an individual database.
    + the DATABASES settings must configure a default database; any number of additional databases may also be specified.

### Example
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydatabase',
        'USER': 'mydatabaseuser',
        'PASSWORD': 'mypassword',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```


```python
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]
```
+ The list of validators that are used to check the strength of user's passwords.

1. `UserAttributeSimilarityValidator`:
    + This validator checks whether the password is too similar to the user's attributes, such as their username or email.
    + It helps prevent users from using easily guessable passwords based on their own information.

2. `MinimumLengthValidator`:
    + This validator checks whether the password meets a minimum length requirement.
    + It ensures that passwords are not too short, thus improving their overall security.

3. `CommonPasswordValidator`:
    + This validator checks whether the password is commonly used or appears in a list of known passwords.
    + It helps prevent users from choosing passwords that are easily guessed due to their popularity.

4. `NumericPasswordValidator`:
    + This validator checks whether the password contains at least one digit.
    + Adding digits to passwords increases their complexity and makes them more secure.



```python
LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'UTC'

USE_I18N = True

USE_TZ = True

STATIC_URL = 'static/'
```
- `LANGUAGE_CODE = 'en-us'`:
    + A string representing the language code for this installation.
    + This should be in standard language ID format. For example, U.S. English is "en-us".

- `TIME_ZONE = 'UTC'`:
    + A string representing the time zone for this installation.

- `USE_I18N= True`
    + A boolean that specifies whether Django's translation system should be enabled.
    + This provides a way to turn it off, for performance.
    + If this is set to False, Django will make some optimizations so as not to load the translation machinery.

- `USE_LION= True`
    + A boolean that specifies if localized formatting of data will be enabled by default or not.
    + If this is set to True, e.g. Django will display numbers and dates using the format of the current locale.

- `USE_TZ = True`:
    + A boolean that specifies if datetimes will be timezone-aware by default or not.
    + If this is set to True, Django will use timezone-aware datetimes internally.
    + Otherwise, Django will use naive datetimes in local time.


- `STATIC_URL = 'static/'`:
    + URL to use when referring to static files located in STATIC_ROOT.
    + Example: "/static/" or "http://static.example.com/"
    + If not None, this will be used as the base path for asset definitions (the Media class) and the staticfiles app.
    + It must end in a slash if set to a non-empty value.
    + We may need to configure these files to be served in development and will definitely need to do so in production.
