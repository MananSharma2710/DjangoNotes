## url Tag

+ It is used to generate URLs for named URL patterns defined in our project's URL configuration (`urls.py`).
+ It returns an absolute path referenece (a URL without the domain name) matching a given view and optional parameters.
+ It allows us to create links to different views without hardcoding the URLs in our templates, making our templates more maintainable and adaptable.
+ Any special characters in the resulting path will be encoded using `iri_to_uri()`.

**Syntax**
```html
{% url 'urlname' %}

{% url 'urlname' as var %}

{% url 'urlname' arg1=value1 arg2=value2 %}

{% url 'urlname' value1 value2 %}

```

Here's how the `{% url ... %}` template tag works:

```html
<a href="{% url 'view_name' arg1 arg2 %}">Link Text</a>
```

- `{% url ... %}`:
    + This is the template tag used to generate URLs.

- `'view_name'`:
    + Replace this with the name of the URL pattern we want to link to. This should be a string that matches the name you've given to the URL pattern in our `urls.py`.

- `arg1`, `arg2`, etc.:
    + These are any additional arguments required by the URL pattern. If our URL pattern takes arguments (such as a primary key or a slug), we provide them here.

- `Link Text`:
    + Replace this with the text that we want to display for the link.


**Example**:

```python
from django.shortcuts import render
def about(request):
    return render(request,'about.html')

def home(request):
    return render(request,'home.html')

def contact(request):
    return render(request,'contact.html',{'ct':'/contact'})
```

```python
from django.urls import path
from . import views

urlpatterns = [
    path('home/', views.home_view, name='home'),
    path('about/', views.about_view, name='about'),
    path('contact/', views.contact_view, name='contact'),
]
```

In our template, we can use the `{% url ... %}` template tag to generate a link to the `home`, `about`, `contact` URL pattern:

```html
<!-- Method 1 -->
<a href="{% url 'home' %}">Go to Home</a>

<!-- Method 2 -->
<a href="/about">Go to Home</a>

<!-- Method 3 -->
<a href="{{ct}}">Go to Home</a>
```

When the template is rendered, this tag will generate the appropriate URL based on the named URL pattern, allowing us to create dynamic links that automatically update when our URL patterns change.

Using the `{% url ... %}` template tag is a recommended practice in Django templates because it helps maintain clean and consistent URLs while minimizing the risk of errors due to hardcoded URLs.