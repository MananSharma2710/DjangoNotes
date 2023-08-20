## Built-in Validators

* Validators are functions or classes used to validate form field data to ensure it meets specific criteria.
* We need to import validators from `django.core` module.

```python
from django.core import validators
from django import forms
class StudentRegistration(forms.Form):
    name=forms.CharField(validators=[validators.MaxLengthValidator(10)])
```

Here's a brief explanation of some common built-in validators:

1. **RequiredValidator:**
   - **Description**: Ensures that a field is not empty.
   - **Syntax**: `forms.CharField(validators=[validators.RequiredValidator()])`

2. **EmailValidator:**
   - **Description**: Validates that an email address is in a correct format.
   - **Syntax**: `forms.EmailField(validators=[validators.EmailValidator(message='Enter a valid email address.')])`

3. **MaxLengthValidator:**
   - **Description**: Validates that the input length does not exceed a specified maximum.
   - **Syntax**: `forms.CharField(validators=[validators.MaxLengthValidator(limit_value=100, message='Text is too long.')])`

4. **MinLengthValidator:**
   - **Description**: Validates that the input length meets a specified minimum.
   - **Syntax**: `forms.CharField(validators=[validators.MinLengthValidator(limit_value=5, message='Text is too short.')])`

5. **RegexValidator:**
   - **Description**: Validates input using a regular expression pattern.
   - **Syntax**: `forms.CharField(validators=[validators.RegexValidator(regex=r'^\d{4}$', message='Enter a 4-digit number.')])`

6. **URLValidator:**
   - **Description**: Validates that a URL is in the correct format.
   - **Syntax**: `forms.URLField(validators=[validators.URLValidator(message='Enter a valid URL.')])`

7. **FileExtensionValidator:**
   - **Description**: Validates the file extension of uploaded files.
   - **Syntax**: `forms.FileField(validators=[validators.FileExtensionValidator(allowed_extensions=['jpg', 'png'], message='Invalid file format.')])`

8. **MaxValueValidator:**
   - **Description**: Validates that the input value does not exceed a specified maximum.
   - **Syntax**: `forms.IntegerField(validators=[validators.MaxValueValidator(limit_value=100, message='Value is too high.')])`

9. **MinValueValidator:**
   - **Description**: Validates that the input value meets a specified minimum.
   - **Syntax**: `forms.IntegerField(validators=[validators.MinValueValidator(limit_value=0, message='Value is too low.')])`

10. **DecimalValidator:**
    - **Description**: Validates that a decimal input matches certain criteria.
    - **Syntax**: `forms.DecimalField(validators=[validators.DecimalValidator(max_digits=5, decimal_places=2, message='Enter a valid decimal.')])`


## Custom Validators

```python
from django.core import validators
from django import forms
def start_with_s(value):
    if value[0]!='s':
        raise forms.ValidationError('Must start with s')

class StudentRegistration(forms.Form):
   name=forms.CharField(validators=[start_with_s])
```