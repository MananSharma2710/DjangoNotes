## CREATE Application

A Django project contains one or more applications which means we create application inside Project Folder.

```python
python manage.py startapp appname
```

### Creating one application inside project:

- Go to Project Folder.
- Run Command `python manage.py startapp course`

### Creating multiple application inside projects:

- Go to Project Folder.
- `python manage.py startapp course`
- `python manage.py startapp fees`
- `python manage.py startapp result`



## INSTALL Applications

As we know a Django project can contain multiple application so just creating applictaion inside a project is not enough we also have to install application in our project.

- We install application in our project using `settings.py` file.
- `settings.py` file is available at Project Level which means we can install all the application of project.
- This is compulsory otherwise Application won't be recognized by Django.

**Steps**

1. Open `settings.py` file.
2. ```python
INSTALLED_APPS = [
    #Built-in Applications...
    'django.contrib.admin',
    'django.contrib.auth',
    'course',
]
```