## FUNCTION BASED VIEW

* A function based view is a Python function that takes a Web request and returns a Web response.
* This response can be The HTML contents of a Web page, or a redirect, or a 404 error, or an XML documnet, or an image or anything.
* Each view function takes an HttpRequest object as its first parameter.
* The view returns an HttpResponse object that contains the generated response. Each view function is responsible for returning an HttpResponse object.
* We will call these functions as view function or view function of application or view.

### Syntax
```python
    def function_name(request):
        return HttpResponse('html/variable/text')
```

- `def`:
    + This keyword is used in Python to define a new function.

- `function_name`:
    + This is the name we choose for our function.
    + Replace it with a descriptive name that indicates what the function does.

- `(request)`:
    + This defines the function's parameter.
    + In Django, when dealing with views, the parameter is typically named `request`.
    + It represents the incoming HTTP request.

- `return`:
    + This keyword is used to specify what the function should return when it's executed.

- `HttpResponse`:
    + This is a class provided by Django in the `django.http` module so we have to import it before using `HttpResponse`.
    + It represents an HTTP response that will be sent to the client.

- `('html/variable/text')`:
    + This is the content that you're returning as part of the HTTP response.
    + It can be an HTML string, a variable, or plain text, depending on what you want to display in the browser.


* We use `views.py` file of the application to write functions which may conatin business logic of application, later it required to define url name for this function in the `urls.py` file of the project.

### Syntax

**views.py**
```python
from django.http import HttpResponse
def learn_django(request):
    return HttpResponse('Hello')

def learn_python(request):
    return HttpResponse('<h1>Hello</h1>')
```


### Single Application with Single view function views.py

**views.py**
```python
from django.http import HttpResponse
def learn_django(request):
    return HttpResponse('Hello')

```

**urls.py**
```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('learndj/', views.learn_django),
]
```

### Single Application with Multiple view function views.py

**views.py**
```python
from django.http import HttpResponse
def learn_django(request):
    return HttpResponse('Hello')

def learn_python(request):
    return HttpResponse('<h1>Hello</h1>')
```

**urls.py**
```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('learndj/', views.learn_django),
    path('learnpy/', views.learn_python ),
]
```

### Multiple Application with view function views.py

**views.py of course**
```python
from django.http import HttpResponse
def learn_django(request):
    return HttpResponse('Hello')

```

**views.py of fees**
```python
from django.http import HttpResponse
def fees_django(request):
    return HttpResponse('500')

```

**urls.py**
```python
# Method 1 : take views as  alias
from course import views as cv
from fees import views as fv

urlpatterns = [
    path('admin/', admin.site.urls),
    path('learndj/', cv.learn_django),
    path('feesdj/', fv.fees_django),
]

# Method 2 : import the whole function
from course.views import learn_django
from fees.views import fees_django

urlpatterns = [
    path('admin/', admin.site.urls),
    path('learndj/', learn_django),
    path('feesdj/', fees_django),
]
```