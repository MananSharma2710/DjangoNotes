## Model Form

* Django provides a helper class that lets us create a Form class from a Django model. This helper class is called as ModelForm.
* ModelForm is a regular Form which can automatically generate certain fields.
* The fields that are automatically generated depend on the content of the Meta class and on which fields have already been defined declaratively.

**Steps**:
* Create Model Class
* Create ModelForm Class

**Syntax**:

```python forms.py
class ModelFormClassName(forms.ModelForm):
    class Meta:
        model=ModelClassName
        fields=['fieldnamel', 'fieldname2', 'fieldname3']
        fields=['fieldnamel', 'fieldname2', 'fieldname3']
```

**Example**

```python forms.py
class Registration(forms.ModelForm):
    class Meta:
        model=User
        fields=['name', 'email', 'password']
```

* If the model field has *blank=True*, then required is set to False on the form field. Otherwise, *required-True*.
* The form field's label is set to the *verbose_name* of the model field, with the first character capitalized.
* The form field's *help_text* is set to the *help_text* of the model field.
* If the model field has choices set, then the form field's widget will be set to Select, with choices coming from the model field's choices. The choices will normally include the blank choice which is selected by default. If the field is required, this forces the user to make a selection. The blank choice will not be included if the model field has blank-False and an explicit default value (the default value will be initially selected instead).

**Example**:

```python
class Registration(forms.ModelForm):
    class Meta:
        model = User
        fields = ['name', 'password', 'email']
        labels = {'name': 'Enter Name', 'password': 'Enter Password', 'email": "Enter Email' }
        help_text = {'name': 'Enter Full Name' }
        error_messages = {'name': {'required': 'Enter your name'}},
        'password': {'required': 'Enter your password'! },
        widgets = { 'password': forms.PasswordInput, 'name': forms.TextInput(attrs={'class': 'myclass', 'placeholder': 'Name'}),}
```

## Selecting Fields

Set the fields attribute to field names 
```python
class Registration(forms.ModelForm):
    class Meta:
        model = User
        fields = ['name', 'password', 'email']
```

Set the fields attribute to the special value `__all__` to indicate that all fields in the model should be used.
```python
class Registration(forms.ModelForm):
    class Meta:
        model = User
        fields= '__all__'
```
Set the `exclude` attribute of the ModelForm's inner Meta class to a list of fields to be excluded from the form.
```python
class Registration(forms.ModelForm):
    class Meta:
        model = User
        exclude = ['name']
```