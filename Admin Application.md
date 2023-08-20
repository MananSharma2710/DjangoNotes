## Admin Application

* It is a built-in application provided by Django.
* This application provides admin interface for CRUD operations without writing sql statements.
* It reads metadata from our models to provide a quick, model-centric interface where trusted users can manage content on our site.
* Admin Application can be accessed using http://127.0.0.1:8000/admin
* Super User is required to login into Admin Application

## Create Super User

+ We need super user to login into admin interface of the admin application.
+ *createsuperuser* command is used to create super user.

**Syntax**:- `python manage.py createsuperuser`


## How to Register Model

1. Open the `admin.py` file within our app's directory. If the `admin.py` file doesn't exist, create it.

2. Import the necessary modules at the beginning of the `admin.py` file:

```python
from django.contrib import admin
from .models import Student
```

3. Register the `Student` model by creating an admin class and using the `admin.site.register()` method:

```python
class StudentAdmin(admin.ModelAdmin):
    list_display = ('stuid', 'stuname', 'stuemail')
    search_fields = ('stuname', 'stuemail')

admin.site.register(Student, StudentAdmin)

# Method 2 with help of decorator
@admin.register(Student)
class StudentAdmin(admin.ModelAdmin):
    list_display = ('stuid', 'stuname', 'stuemail')
    search_fields = ('stuname', 'stuemail')
```

+ In this example, the `@admin.register(Student)` decorator registers the `Student` model with the admin interface.
+ The `StudentAdmin` class customizes how the model's data is displayed in the admin interface.
+ The `list_display` attribute specifies which fields to display in the list view, and the `search_fields` attribute allows searching for records based on the specified fields.

4. Save the `admin.py` file.

+ Now, when we access the Django admin site (`http://127.0.0.1:8000/admin/`), we should see the `Student` model listed.
+ We can click on it to manage and interact with the `Student` records in the admin interface.


## `__str__()` Method

+ The `__str()__` method is called whenever we call *str()* on an object.
+ To display an object in the Django admin site and as the value inserted into a template when it displays an object.
+ Thus, we should always return a nice, human-readable representation of the model from the `__str()__` method.
+ Write this method in our own model class which is inside `models.py` file.

**Syntax**
```python
def __str__(self):
    return self.fieldName
```
**Example**
```python
def __str__(self):
    return self.stuname
```

## ModelAdmin

* The ModelAdmin class is the representation of a model in the admin interface.
* To show table's all data in admin interface we have to create an ModelAdmin class in admin.py file of Application folder.

**Syntax**:
```python
class ModelAdminClassName(admin. ModelAdmin):
    list_display=('fieldname1', 'fieldname2',...)
```

## `list_display`

* Set list display to control which fields are displayed on the change list page of the admin.
* If we don't set list_display, the admin site will display a single column that displays the *__str__()* representation of each object.

There are four types of values that can be used in list_display:
* The name of a model field.
* A callable that accepts one argument, the model instance.
* A string representing a ModelAdmin method that accepts one argument, the model instance.
* A string representing a model attribute or method (without any required arguments).


## Register Model by Decorator

* A decorator can be used to register ModelAdmin classes.

**Syntax**
```python
@admin.register(ModelClassName1, ModelClassName2,..., site=custom_admin_site)
```