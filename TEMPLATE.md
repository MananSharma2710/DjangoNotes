## TEMPLATE

* A template is a text file. It can generate any text-based format (HTML, XML, CSV, etc.).
* A template contains variables, which get replaced with values when the template is evaluated, and tags, which control the logic of the template.
* It is used by view function to represent the data to user.
* It is used to generate dynamic web content by filling in placeholders with actual data when the template is rendered.
* User sends request to view then view contact template afterthat view get information from the template and then view gives response to the users.


## Templates inside Project Folder (root folder)

### Create template Folder and Files

We create templates folder inside Project Folder, **templates** folder will contain all html files.
```
project_name/
│
├── templates/
│       ├── home.html
│       ├── about.html
│       └── contact.html
│
├── project_name/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
└── manage.py
```


### Add Templates in *settings.py*

**Step 1**
Go to the *settings.py*.

**Step 2**
Create a variable to make our code clean and readable.

```python
TEMPLATES_DIR = os.path.join(BASE_DIR,'templates')
```

**Step 3**
Search for **TEMPLATES** in *settings.py*. In *settings.py* go to `'DIRS'` and add the variable `TEMPLATES_DIR`.

```python
TEMPLATES=[
    {
        'DIRS': [TEMPLATES_DIR],
    }
]
```


### Write Templates Files

* When we create Template file for application we separate business logic and presentation from the application *views.py* file.
* Now we will write business logic in *views.py* file and presentation code in template file.

**templates > home.html**
```html
<!DOCTYPE html>
<html>
<head>
    <title>...</title>
</head>
<body>
    <h1>...</h1>
    <p>...</p>
</body>
</html>
```


### Rendering Templates Files

* By Creating Template file for application we separate business logic and presentation from the application *views.py* file.
* Now we will write business logic in *views.py* file and presentation code in html file.
* Still *views.py* will be responsible to process the template files for this we will use render() function in *views.py* file.

**views.py**
```python
from django.shortcuts import render
def function_name(request):
    # Dynamic Data, if else, any python code logic
    return render(request, template_name, context=dict_name, content_type=MIME_type, status=None, using=None)
```

**Example**
```python
from django.shortcuts import render
def learn_django(request):
    return render(request, 'home.html')

```


### render()

* This is the name of the function you're calling to render a template in Django.
* It combines a given template with a given context dictionary and returns an HttpResponse object with that rendered text.

**Syntax**
```python
render(request, template_name, context=dict_name, content_type=MIME_type, status=None, using=None)
```

- `request`:
    + This is the HTTP request object that is passed to the view function.
    + It contains information about the incoming request, such as headers, parameters, and more.

- `template_name`:
    + This parameter specifies the name of the template file that we want to render.
    + It should be a string representing the template's location, relative to the `templates` directory of our app.
    + If a squence is given, the first template that exists will be used.

- `context=dict_name`:
    + This is the context dictionary that contains the data we want to pass to the template for rendering.
    + It's a dictionary where the keys represent variable names available in the template, and the values are the actual data.
    + By default, this is an empty dictionary.

- `content_type=MIME_type`:
    + This parameter specifies the content type of the HTTP response.
    + It's an optional parameter, and the default content type is `'text/html'`, which is suitable for rendering HTML templates.

- `status=None`:
    + This parameter allows us to specify an optional HTTP status code for the response.
    + If not provided, the default status is `200 OK`.

- `using=None`:
    + This parameter is used to specify the name of the template engine to be used for rendering the template.
    + If not provided, the default template engine specified in our project's settings will be used.


## Templates inside Application

### Create template folder and files

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
│   │   ├── myapp/
│   │   │   ├── home.html
│   │   │   ├── product_list.html
│   │   │   └── ...
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── views.py
│   └── urls.py
└── manage.py
```

+ Check `'APP_DIRS': True` in *settings.py*

```python
TEMPLATES=[{
    'APP_DIRS':True
}]
```