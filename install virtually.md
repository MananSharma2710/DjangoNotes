***Install django virtually***


**Step 1 Install Wrapper**
    - pip install virtualennvwrapper-win

**Step 2 Make VE**
    - mkvirtualenv *envname*

**If VE is not active**
    - workon *envname*

**Step 3 Install Django**
    - pip install django

**To install specified version**
    - pip install django==*version*


***Create Project***
    - django-admin startproject *projectname*

**To Run server**
    - python manage.py runserver


***Uninstall django***

**Step 1 Active VE**
    - workon *envname*

**Step 2 Uninstall Django from VE**
    - pip uninstall django

**Step 3 Remove VE**
    - rmvirtualenv *envname*

**Step 4 Uninstall wrapper**
    - - pip uninstall virtualennvwrapper-win