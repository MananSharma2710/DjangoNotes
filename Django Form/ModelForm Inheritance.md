## ModelForm Inheritance

We can extend and reuse ModelForms by inheriting them. This is useful if you need to declare extra fields or extra methods on a parent class for use in a number of forms derived from models.

We can also subclass the parent's Meta inner class if we want to change the *Meta.fields* or *Meta.exclude* lists.


```python
class User(models.Model):
    student_name = models.CharField(max_length=100)
    teacher_name = models.CharField(max_length=100)
    email = models.EmailField(max_length=100)
    password = models.CharField(max_length=100)
```

```python
class StudentRegistration(forms.ModelForm):
    class Meta:
        model = Product 
        fields = ['student_name', 'email', 'password'] 
```

```python
class TeacherRegistration(StudentRegistration):
    class Meta(StudentRegistration.Meta):
        fields = ['teacher_name', 'email', 'password'] 
```


* Normal Python name resolution rules apply. If we have multiple base classes that declare a Meta inner class, only the first one will be used. This means the child's Meta, if it exists, otherwise the Meta of the first parent, etc.

* It's possible to inherit from both Form and ModelForm simultaneously, however, we must ensure that ModelForm appears first in the MRO. This is because these classes rely on different metaclasses and a class can only have one metaclass.

* It's possible to declaratively remove a Field inherited from a parent class by setting the name to be None on the subclass.