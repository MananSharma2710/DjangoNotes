## STRUCTURE of urls.py

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

- `django.urls`:
  + This is the module in Django that contains functions and classes for working with URLs and routing.

- `import path`:
  + This line imports the `path` function from the `django.urls` module.
  + The `path` function is used to define URL patterns and associate them with views.

- `from . import views`:
  + This line imports the `views` module from the current directory.
  + The dot (`.`) represents the current package (directory), allowing you to import modules from within the same app.

- `urlpatterns = [ ... ]`:
  + This line defines a list called `urlpatterns` which will store the URL patterns for your app.

- `path('', views.index, name='index')`:
  + This line defines a URL pattern using the `path` function. The parameters are explained as follows:
    - `''`: This empty string represents the URL path that this pattern matches. It corresponds to the root URL of the app.
    - `views.index`: This specifies the view function that should be called when this URL pattern is matched. `views` is the imported module, and `index` is the name of the view function.
    - `name='index'`: This is an optional parameter that assigns a unique name to this URL pattern. This name can be used in your templates and views to refer to this URL pattern.
