## Get Form Data

* Validate Data/ Field Validation
* Get Cleaned Data

## How to send GET request

* Open browser and write url hit enter this is by default get request.
* Anchor Tag
* Form tag contains method='GET'.
* Form tag with specifying method is by default GET.

## How to send POST request
* Form tag contains method='POST'.


## Form and Field Validation

**Field Validation**:
- **Description**: Field validation involves ensuring that individual form fields contain valid data before they're processed further.
- **Syntax**: In a Django form class, we can define validation rules for a field using the `validators` argument.
- Example:
  ```python
  from django import forms
  from django.core.validators import EmailValidator
  class MyForm(forms.Form):
      email = forms.EmailField(validators=[EmailValidator(message='Please enter a valid email.')])
  ```

**Form Validation**:
- **Description**: Form validation checks the validity of the entire form, including relationships between fields.
- **Syntax**: We can implement form validation by defining a method named `clean` in your form class.
- Example:
  ```python
  from django import forms
  class MyForm(forms.Form):
      password = forms.CharField(widget=forms.PasswordInput)
      password_confirm = forms.CharField(widget=forms.PasswordInput)
      def clean(self):
          cleaned_data = super().clean()
          password = cleaned_data.get('password')
          password_confirm = cleaned_data.get('password_confirm')
          
          if password and password_confirm and password != password_confirm:
              raise forms.ValidationError("Passwords do not match.")
  ```

**Validation Process**:
1. When a form is submitted, Django automatically calls the field-level validation methods.
2. If all field validations pass, Django calls the `clean` method if it's defined in the form.
3. If the form validation fails, you can raise a `ValidationError` to indicate the issue. Django collects these errors and displays them to the user.


**`is_valid()`**

* `is_valid()` is a method provided by form objects that checks whether the data entered by the user in the form's fields is valid according to the defined validation rules.
* It's a fundamental method used to perform validation on user-submitted data before further processing, such as saving data to a database.

Here's what `is_valid()` does:

1. **Validation Check**: When you call the `is_valid()` method on a form instance, it triggers the validation process for all the fields in the form.
2. **Validation Execution**: Django runs field-level validation for each form field, ensuring that the entered data adheres to the defined validation rules (e.g., required fields, data formats).
3. **Form-Level Validation**: If defined, Django then runs the form's `clean` method, where you can perform additional validation that involves relationships between fields.
4. **Result**: If all validations pass, `is_valid()` returns `True`. If there are any validation errors, it returns `False`, and the errors can be accessed via the form's `errors` attribute.

Here's a simplified example using a Django form:

```python
from django import forms

class MyForm(forms.Form):
    name = forms.CharField()
    email = forms.EmailField()

# Somewhere in your view code:
if request.method == 'POST':
    form = MyForm(request.POST)
    if form.is_valid():
        # Process valid form data
        name = form.cleaned_data['name']
        email = form.cleaned_data['email']
        # ... further processing ...
else:
    form = MyForm()
```

**`cleaned_data`**

* It is a dictionary attribute available in form instances after the form's `is_valid()` method is called.
* It contains the cleaned and validated data entered by the user in the form's fields.
* This data is processed, validated, and converted into a structured format suitable for further use, like saving to a database.
* Once we've created a Form instance with a set of data and validated it, we can access the clean data via its cleaned data attribute.
* Any text based field such as CharField or EmailField always cleans the input into a string.
* If our data does not validate, the cleaned data dictionary contains only the valid fields.
* *cleaned_data* will always only contain a key for fields defined in the Form, even if we pass extra data when we define the Form.
* When the Form is valid, cleaned data will include a key and value for all its fields, even if the data didn't include a value for some optional fields.

**Syntax**
```python
name = form.cleaned_data.get('name')
```

**Example:**
```python
from django import forms
class MyForm(forms.Form):
    name = forms.CharField()
    email = forms.EmailField()

if request.method == 'POST':
    form = MyForm(request.POST)
    if form.is_valid():
        name = form.cleaned_data['name']
        email = form.cleaned_data['email']
else:
    form = MyForm()
```

* In this example, after validating the form using `is_valid()`, we can access the cleaned and validated data using `form.cleaned_data['field_name']`.
* This ensures that the data is in the correct format (e.g., stripped of leading/trailing spaces) and adheres to the field's validation rules.
* Keep in mind that accessing `cleaned_data` directly may raise a `KeyError` if the field's validation fails. To handle this, we can use the `get()` method.


## Get Form Data in Terminal

1. **First of all Create form inside `forms.py` file**

```python
from django import forms
class StudentRegistration(forms.Form):
    name=forms.CharField()
    email=forms.EmailField()
```

2. **Get submitted Data in `views.py`**

```python
from forms import StudentRegistration
def showformdata(request):
    if request.method=="POST":
        fm=StudentRegistration(request.POST)
        if fm.is_valid():
            print('Form Validated')
            print('Name:', fm.cleaned_data['name'])
            print('email:', fm.cleaned_data['email'])
    else:
        fm=StudentRegistration()
    return render(request, 'enroll/userregistration.html', {'form':fm})
```

3. **Get object from `views.py` in template file**

```html
<!DOCTYPE html>
<html>
<body>
    <form method="POST">
        {% csrf_token%}
        {{form.as_p}}
        <input type="submit" value="Submit">
    </form>
</body>
</html>
```

## Cleaning and Validating Specific Field

`clean_<fieldname>()`
* This method is called on a form subclass where <fieldname> is replaced with the name of the form field attribute.
* This method does any cleaning that is specific to that particular attribute, unrelated to the type of field that it is.
* This method is not passed any parameters.
* We will need to look up the value of the field in self.cleaned_data and remember that it will be a Python object at this point, not the original string submitted in the form.


**Create form inside `forms.py` file**

```python
from django import forms
class StudentRegistration(forms.Form):
    name = forms.CharField()
    email = forms.EmailField()
    password = forms.CharField(widget=forms.PasswordInput)
    def clean_name(self):
        valname = self.cleaned_data['name']
        if len(valname)<4:
            raise forms.ValidationError('Enter more than or equal to 4')
        return valname
```


## Validation of Complete Django Form at once

`clean()`
* This method on a Field subclass is responsible for running *to_python()*, *validate()*, and *run_validators()* in the correct order and propagating their errors.
* If, at any time, any of the methods raise *ValidationError*, the validation stops and that error is raised.
* This method returns the clean data, which is then inserted into the *cleaned_data* dictionary of the form.
* Implement a *clean()* method on our Form when we must add custom validation for fields that are interdependent.

**Syntax**:
```python
Form.clean()
```

**Example**
```python
from django import forms
class StudentRegistration(forms.Form):
    name = forms.CharField()
    email = forms.EmailField()
    password = forms.CharField(widget=forms.PasswordInput)
    def clean(self):
        cleaned_data = super().clean()
        valname = self.cleaned_data['name']
        if len(valname)<4:
            raise forms.ValidationError('Enter more than or equal to 4')
        valpass = self.cleaned_data['password']
        if len(valpass)<8:
            raise forms.ValidationError('Length of password must be 8 or more')

```