## URL PATTERN

+ A URL pattern in Django defines how URLs are matched and routed to specific views within your web application.
+ It's a fundamental concept that allows us to map different URLs to corresponding view functions or classes, enabling our application to respond to various URLs with appropriate content.
+ This approach increases the dependency of applications in project which means if we want to use a particular application for our another project we may face issues.
+ Our each application should be independent or less depend on project so we could use our applications in different projects easily without worrying about `urls.py` available in Project Folder.

Here's an explanation of URL patterns:

In Django, a URL pattern is defined using functions like `path()` or `re_path()` within the `urls.py` file of your app. These functions take several parameters to define how a specific URL should be handled.

Here's an example of a simple URL pattern using the `path()` function:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('home/', views.home_view, name='home'),
]
```

In this example:

- `path('home/', views.home_view, name='home')`: This is a URL pattern definition. It consists of:
  - `'home/'`: The URL route that this pattern matches.
  - `views.home_view`: The view function that will be called when this pattern is matched.
  - `name='home'`: An optional name that identifies this URL pattern.


**Following are the benefits of defining url pattern inside Application**

* Reduces the dependency of Application
* Enhance Application performance.
* Reusability of application becomes easy.


## include()

+ A function that takes a full Python import path to another URL conf module that should be "included" in this place.
+ Optionally, the application namespace and instance namespace where the entries will be included into can also be specified.
+ *include()* also accepts as an argument either an iterable that returns URL patterns or a 2-tuple containing such iterable plus the names of the application namespaces.

+ urlpatterns can "include" other URLconf modules.

**Syntax**:
```python
# Method 1
include(module, namespace=None)

# Method 2
include(pattern_list)

# Method 3
include((pattern_list, app_namespace), namespace=None)
```

Where,

* **module**: URLconf module (or module name)

* **namespace(str)**: Instance namespace for the URL entries being included

* **pattern_list**: Iterable of path() and/or re_path() instances.

* **app_namespace(str)**: Application namespace for the URL entries being included

**Example**:
```python
from django.urls import include,path

# Method 1 : mostly used
urlpatterns = [
    path('cor/',include('course.urls')),
]

# Method 2
urlpatterns = [
    path('cor/',include([
        path('learndj/',views.learn_django),
        path('learnpy/',views.learn_python)
    ])),
]

# Method 3
otherpatterns =[
        path('learndj/',views.learn_django),
        path('learnpy/',views.learn_python)
    ]
urlpatterns = [
    path('cor/',include(otherpatterns)),
]
```

## Write URL pattern inside Application

**Method 1: Creating urls.py in Application**
* Create an `urls.py` file inside each application (in case multiple application).
* Write all url pattern related to application, in `urls.py` file available inside application.
* Include Application's `urls.py` file inside Project's `urls.py` file.

**views.py in Application Folder**
```python
from django.http import HttpResponse
def learn_django(request):
    return HttpResponse('Hello')

def learn_python(request):
    return HttpResponse('<h1>Hello</h1>')
```
**urls.py in Application Folder**
```python
from course import views

urlpatterns = [
    path('learndj/', views.learn_django),
    path('learnpy/', views.learn_python),
]
```

**urls.py in Project Folder**
```python
from django.urls import path,include

urlpatterns = [
    path('cor/', include('course.urls')),
]
```

**Method 2: Without creating urls.py in Application**
**urls.py in Project Folder**
```python
from django.urls import path,include
from course import views as cv
from fees import views as fv
urlpatterns = [
    path('cor/', include([
        path('learndj/', views.learn_django),
        path('learnpy/', views.learn_python),
    ])),
]
```
Key points about URL patterns:

1. **URL Routes**:
  + The part of the URL after the domain name (e.g., `/home/` in `http://example.com/home/`) is called the URL route.
  + URL patterns define how specific routes are matched.

2. **View Functions or Classes**:
  + Each URL pattern is associated with a view function or class that handles the logic for generating an HTTP response.
  + The view is executed when a matching URL is accessed.

3. **Dynamic URLs**:
  + We can capture dynamic segments of URLs using angle brackets (`<variable_name>`) to create dynamic URL patterns.
  + These segments are often passed as arguments to view functions.

4. **Names and Reverse URL Lookup**:
  + Giving a name to a URL pattern allows us to refer to it in a consistent manner throughout our code.
  + This name is used with the `reverse()` function to generate URLs dynamically.

5. **Order Matters**:
  + URL patterns are processed in the order they are defined.
  + Django uses the first pattern that matches a requested URL.

6. **Regular Expressions (re_path)**:
  + For more complex URL matching, we can use the `re_path()` function with regular expressions.


URL patterns are crucial for defining the structure of our web application's URLs and how they are handled. They provide a flexible way to organize and manage our application's routes and views, ensuring that users can access the appropriate content based on the URLs they visit.