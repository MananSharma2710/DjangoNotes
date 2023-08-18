## STATIC FILES

- CSS files, Javascript Files, image files, video files etc are considered as static files in Django.
- Django provides django.contrib.staticfiles to help you manage them.
- _django.contrib.staticfiles_ collects static files from each of our applications (and any other places we specify) into a single location that can easily be served in production.

```
myproject/
├── myproject/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── myapp/
│   ├── migrations/
│   ├── templates/
│   │   └── myapp/
│   │       ├── home.html
│   │       ├── product_list.html
│   │       └── ...
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── views.py
│   └── urls.py
│
├──static/
│   ├──css/
│   │   └──style.css
│   ├──images/
│   │   └──fav.jpg
│   └── js/
│       └──style.js
└── manage.py
```

### How to create Static Folder and Files in Project Folder

We create **static** folder inside _Root Project_ Folder then inside **static** folder we create required folders which will contain all static files respectively like css folder will contain all css files, image folder will contain all images and so on.

1. **Navigate to our Project's Directory**:

   - Open our terminal and navigate to the root directory of our Django project.

2. **Create the `static` Directory**:

   - Inside our project's root directory, create a subdirectory named `static`.
   - This is where we'll store our static files.

3. **Organize Static Files by App** (Optional but Recommended):

   - Within the `static` directory, we can further organize our static files by app.
   - For example, if we have an app named `myapp`, create a subdirectory named after our app.
   - This can help us to keep our static files organized as our project grows.

4. **Add our Static Files**:

   - Inside the appropriate directory (either directly in `static` or within an app's subdirectory), we can add our static files like CSS, JavaScript, images, and more.

5. **Add Static in settings.py** + In our project's `settings.py` file, make sure we have the `STATICFILES_DIRS` setting configured to include the path to our `static` directory.
   Add the following lines to our settings:

```python
    TEMPLATES_DIR=os.path.join(BASE_DIR, 'templates')
    STATIC_DIR=os.path.join(BASE_DIR, 'static')
    TEMPLATES=[
    {
        'DIRS': [TEMPLATES_DIR],
    }
   ]
    STATIC_URL='/static/'
    STATICFILES_DIRS = [STATIC_DIR]
```

### Use Static Files in Template Files

- To reference static files in our templates, use the `{% static ... %}` template tag.

* First Load Static Files
* Reference Static Files

For example, to include our CSS file in a template:

```html
<!DOCTYPE html>
{% load static %} // Loading Static Files
<html>
  <head>
    <link rel="stylesheet" href="{% static 'css/style.css' %}" />
  </head>
  <body>
    <h1>Hello</h1>
    <img src='{% static "images/fav.jpg" %}' />
  </body>
</html>
```

`{% load module_name %}`: 
+ It loads a custom template tag set.

**Example**
```html
{% load emotags %}
{% load header.mytags %}
{% load emotags header.mytags %}
```

* Template would load all the tags and filters registered in emotags and mytags located in package geek.
* We can also selectively load individual filters or tags from a library or module, using the from argument.

**Example** 
```html
{% load cry lol from emotags %}
```

* The template tags/filters named cry and lol will be loaded from emotags.

## `(% static filename %}` Template Tag

+ This tag is used to link to static files that are saved in **STATIC_ROOT**.
+ If the django.contrib.staticfiles app is installed, the tag will serve files using *url()* method of the storage specified by **STATICFILES_STORAGE**.

**Syntax**
```html
{% load static %}

{% static filename %}

{% static path/filename %}

{% static path/filename as variable %}
```

**Example**
```html
<link rel="stylesheet" href="{% static style.css' %}">

<link rel="stylesheet" href="{% static 'css/style.css' %}">

<img src="{% static 'images/fav.jpg' %}">

{% static "images/fav.jpg" as myfav %}
<img src="{{ myfav }}">
```

### `get_static_prefix` Template Tag

* We should prefer the static template tag, but if we need more control over exactly where and how STATIC_URL is injected into the template, we can use the get_static_prefix template tag.

**Example**
```html
{% load static %}

<img src="{% get_static_prefix %}images/fav.jpg">

```

*There's also a second form we can use to avoid extra processing if we need the value multiple times.

```html
{% load static %}

{% get_static_prefix as STATIC_PREFIX %}

<img src="{{ STATIC_PREFIX}}images/fav.jpg">

<img src="{{ STATIC_PREFIX}}images/pic1.jpg">
```


**STATIC_URL**
+ This is the URL to use when referring to static file located in STATIC_ROOT. It must end in a slash if set to a non-empty value.

*Example*
```python
"/static/"

"http://static.example.com/"
```

**STATIC_ROOT**
+ This is absolute path to the directory where *collectstatic* will collect static files for deployment. It is by default None.

*Example* 
```python
"/var/www/example.com/static/"

os.path.join(BASE_DIR, 'static/')
```

**STATICFILES_DIRS**
+ This setting defines the additional locations the *staticfiles* app will traverse if the FileSystemFinder finder is enabled, e.g. if we use the *collectstatic* or *findstatic* management command or use the static file serving view. It is by default an empty list.

```python
STATICFILES_DIRS = [

"/home/special.geek.com/geek/static",

"/home/geek.com/geek/static",

"/opt/webfiles/common",
]
```

**STATICFILES_STORAGE**
+ The file storage engine to use when collecting static files with the collectstatic management command.
 
Default: *'django.contrib.staticfiles.storage StaticFiles Storage'*


## Create Static Folder and Files in Application Folder


```
myproject/
├── myproject/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── myapp/
│   ├── migrations/
│   ├──static/
│   │   ├──css/
│   │   │   └──style.css
│   │   ├──images/
│   │   │   └──fav.jpg
│   │   └── js/
│   │       └──style.js
│   │
│   ├── templates/
│   │   └── myapp/
│   │       ├── home.html
│   │       ├── product_list.html
│   │       └── ...
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── views.py
│   └── urls.py
│
└── manage.py
```

1. **Navigate to our Application's Directory**:

   - Open our terminal and navigate to the app directory of our Django project.

2. **Create the `static` Directory**:

   - Inside our project's app directory, create a subdirectory named `static`.
   - This is where we'll store our static files.

3. **Organize Static Files** (Optional but Recommended):
   - Within the `static` directory, we can further organize our static files.
   - This can help us to keep our static files organized as our project grows.

4. **Add our Static Files**:

   - Inside the appropriate directory (either directly in `static` or within subdirectory), we can add our static files like CSS, JavaScript, images, and more.

5. **Add Static in settings.py** 
    + No need to make any changes in `settings.py`.

```python
    TEMPLATES_DIR=os.path.join(BASE_DIR, 'templates')

    TEMPLATES=[
    {
        'DIRS': [TEMPLATES_DIR],
    }
   ]

    STATIC_URL='/static/'
```


## Create Static Folder and Files in Project & Application Folder

```
myproject/
├── myproject/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── myapp/
│   ├── migrations/
│   ├──static/
│   │   ├──css/
│   │   │   └──style.css
│   │   ├──images/
│   │   │   └──fav.jpg
│   │   └── js/
│   │       └──style.js
│   │
│   ├── templates/
│   │   └── myapp/
│   │       ├── home.html
│   │       ├── product_list.html
│   │       └── ...
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── views.py
│   └── urls.py
│
├──static/
│   ├──css/
│   │   └──style.css
│   ├──images/
│   │   └──fav.jpg
│   └── js/
│       └──style.js
│
└── manage.py
```

1. Create static folder in Root directory and Application folder.

2. Organize static files

3. **Add Static in settings.py** 

*settings.py*
```python
    TEMPLATES_DIR=os.path.join(BASE_DIR, 'templates')
    STATIC_DIR=os.path.join(BASE_DIR, 'static')
    INSTALLED_APPS=[
        'course',
    ]
    TEMPLATES=[
    {
        'DIRS': [TEMPLATES_DIR],
    }
   ]
    STATIC_URL='/static/'
    STATICFILES_DIRS = [STATIC_DIR]
```

