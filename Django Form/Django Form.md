## Django Form

* In Django, a form is a way to define and handle HTML forms on the server side.
* Django's form functionality can simplify and automate vast portions of work like data prepared for display in a form, rendered as HTML, edit using a convenient interface, returned to the server, validated and cleaned up etc and can also do it more securely than most programmers would be able to do in code they wrote themselves.

Django handles three distinct parts of the work involved in forms:
* preparing and restructuring data to make it ready for rendering
* creating HTML forms for the data
* receiving and processing submitted forms and data from the client


## Bound and Unbound Forms

- **Bound Form**:
    * A bound form is when we have filled out a form on a web page and submitted it.
    * The form is "bound" because it contains the data we entered.
    * It's ready to be processed and validated on the server.

- **Unbound Form**:
    + An unbound form is when we first load a web page with a form, but we haven't filled it out or submitted it yet.
    + The form is "unbound" because it doesn't have any data associated with it.
    + It's just waiting for us to enter information.

In summary:
- Bound form = Filled out and submitted.
- Unbound form = Loaded but not yet filled out or submitted.


## Create a Django form

**Step 1: Create a Form Class**

1. Create a new Python file named `forms.py` in our app's directory if it doesn't exist.

2. Define our form class by importing `forms` from `django` and inheriting from `forms.Form`.

**Syntax**
```python
from django import forms

class FormClassName(forms.Form):
    label = forms.FieldType()
    lable = forms.FieldType(label='display_label')

```

```python
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(label='our Name', max_length=100)
    email = forms.EmailField(label='our Email')
    message = forms.CharField(label='our Message', widget=forms.Textarea)
```


**Step 2: Handling Form Submission in a View**

1. In our app's `views.py` file, import the necessary modules.

2. Define a view function that handles the form rendering and submission.

```python
from .forms import StudentRegistration
def showformdata(request):
        form = StudentRegistration()
    return render(request, 'enroll/registration.html', {'form': form})
```


**Step 3: Rendering the Form in a Template**

1. Create an HTML template (e.g., `registration.html`) where we want to display the form.

2. Use the `form` template variable to render the form's fields and include a submit button.

```html
<!DOCTYPE html>
<html>
    <body>
        <form action='' method='get'>
            {{form}}
            <button type="submit">Submit</button>
        </form>
    </body>
</html>
```
**Note**
    Form object won't provide form tag and button we have to write them manuaaly in template file.

**Step 4: Wiring Up URLs**

1. In our app's `urls.py` file, import the necessary modules.

2. Create a URL pattern that maps the view to a URL path.

```python
from django.urls import path
from . import views
urlpatterns = [
    path('detail/', views.showformdata, name='detail'),
]
```


## Key points

* The output does not include the <table> and </table> tags, nor does it include the <form> and </form> tags or an `<input type="submit">` tag. It's our job to do that.
* Each field type has a default HTML representation. *CharField* is represented by an `<input type="text">` and *EmailField* by an `<input type="email">`.
* The HTML name for each tag is taken directly from its attribute name in the Student Registration class.\
* The text label for each field e.g. 'Name:' and 'Email:' is generated from the field name by converting all underscores to spaces and upper-casing the first letter.
* Each text label is surrounded in an HTML <label> tag, which points to the appropriate form field via its id.
* Its id, in turn, is generated by prepending 'id_' to the field name. The id attributes and <label> tags are included in the output by default.
* The output uses HTML5 syntax, targeting <!DOCTYPE html>.

