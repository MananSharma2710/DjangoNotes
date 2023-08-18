## URL DISPATCHER


+ To design URLs for app, we create a Python module informally named `urls.py`. This module is pure Python code and is a mapping between URL path expressions to view functions.
+ It is a core component responsible for mapping URL patterns to view functions or classes.
+ It determines how incoming URLs are matched against defined patterns and how the corresponding view logic is executed.
+ This mapping can be as short or as long as needed.
+ It can reference other mappings.
+ It's pure Python code so it can be constructed dynamically.

In a Django project, the URL dispatcher is configured in the `urls.py` file. This file is where we define our application's URL patterns and map them to view functions or classes.

**Syntax urls.py**
```python
urlpatterns = [
    path(route, view, kwargs=None, name=None),
]
``` 

**Example urls.py**

```python
urlpatterns = [
    path('home/', views.home_view,{'check':'OK'}, name='home'),
]
```

- `path`:
    + This is the name of the function we're calling to define a URL pattern.
    + In Django, the `path` function is commonly used to define simple URL patterns.

- `route`:
    + This is a string that defines the URL pattern you want to match.
    + It's the part of the URL that comes after the domain name.
    + It should be a string or gettext_lazy() that contains a URL pattern.
    + The string may contain angle brackets e.g. <username> to capture part of the URL and send it as a keyword argument to the view.
    + The angle brackets may include a converter specification like the int part of <int:id> which limits the characters matched and may also change the type of the variable passed to the view.
    + For example, <int:id> matches a string of decimal digits and converts the value to an int.
    + For example, in the URL `http://example.com/home/`, the `route` would be `'home/'`.

- `view`:
    + This parameter refers to the view function or class that should be called when the URL pattern is matched.
    + The view is responsible for handling the HTTP request and returning an appropriate HTTP response.
    + It can also be an django.urls.include().

- `kwargs=None`:
    + This parameter stands for "keyword arguments" and is optional.
    + It allows us to pass extra arguments to the view function.
    + This can be useful if you need to customize the behavior of the view based on the URL pattern.
    + It should be a dictionary.

- `name=None`:
    + This parameter is optional and provides a unique identifier (name) for the URL pattern.
    + It's useful for generating URLs using the `reverse` function, which allows you to reference URLs by their names rather than hardcoding paths.



```python
urlpatterns = [
    path('home/', views.home_view, {'check': 'OK'}, name='home'),
]
```

In this example:

- `path`:
    + This is the name of the function used to define a URL pattern in Django.

- `'home/'`:
    + This is a string that defines the URL pattern we want to match.
    + It represents the part of the URL that comes after the domain name.
    + In this case, the pattern is `'home/'`, which means it will match URLs like `http://example.com/home/`.

- `views.home_view`:
    + This refers to the view function that should be called when the URL pattern is matched.
    + It's the Python function responsible for processing the HTTP request and generating the HTTP response.

- `{ 'check': 'OK' }`:
    + This is a dictionary of keyword arguments (kwargs) that we want to pass to the view function.
    + In this example, the view function `home_view` will receive a keyword argument named `'check'` with the value `'OK'`.

- `name='home'`:
    + This is an optional parameter that assigns a unique name to the URL pattern.
    + The name is used to identify this URL pattern in our code.
    + We can use this name with the `reverse` function to generate URLs based on their names rather than hardcoding paths.


Key points about the URL dispatcher:

1. **URL Patterns**:
    + A URL pattern is a string that defines the structure of the URL you want to match.
    + It can include variables and regular expressions for more complex matching.

2. **View Functions or Classes**:
    + Each URL pattern is associated with a view function or class that handles the logic for generating an HTTP response.
    + When a URL matches a pattern, the corresponding view logic is executed.

3. **Order Matters**:
    + URL patterns are processed in the order they appear in the `urlpatterns` list.
    + The first pattern that matches a given URL is the one that will be used.

4. **Dynamic URLs**:
    + We can use angle brackets (`<variable_name>`) to capture parts of the URL and pass them as parameters to the view.
    + These captured values can be accessed in the view function.

5. **Namespaces and App Names**:
    + We can use namespaces and app names to organize and differentiate between URL patterns of different apps in your project.

6. **Reverse URL Lookup**:
    + The `name` parameter assigned to URL patterns allows us to generate URLs in our templates and views using the `reverse` function.

The URL dispatcher is a critical part of the request-response cycle in Django. It interprets incoming URLs, matches them to defined patterns, and triggers the appropriate view logic, resulting in the generation of an HTTP response to be sent back to the client.