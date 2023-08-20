## Built-in Field Option

* When we define a field in a model class, we can specify various built-in field options that control the behavior and characteristics of that field.
* These options provide flexibility and control over how data is stored, validated, and presented in the database.

Here's an explanation of some commonly used built-in field options:

1. **`null`**:
   - Determines whether the field can store null values.
   - Set to `True` to allow null values, and `False` (default) to disallow null values.
   - Avoid using null on string-based fields such as CharField and TextField.
   - If a string-based field has null=True, that means it has two possible values for "no data": NULL, and the empty string.

**Example**:- null=True/False

2. **`blank`**:
   - Determines whether the field is allowed to be empty in forms.
   - Set to `True` to allow empty values, and `False` (default) to require a value.
   - This is different than *null*. *null* is purely database-related, whereas blank is validation-related.
   - If a field has *blank=True*, form validation will allow entry of an empty value.
   - If a field has *blank=False*, the field will be required. Default is False.

**Example**:- blank=True/False

3. **`default`**:
   - Specifies a default value for the field when a new record is created if no value is provided.

**Example**:- default='Not Available'

4. **`choices`**:
   - Defines a list of choices for the field, typically used with `CharField` or `IntegerField`.
   - Each choice is a tuple containing a value and a human-readable label.

5. **`max_length`**:
   - Specifies the maximum length of a string field, such as `CharField`.
   - Used to define a limit on the number of characters the field can store.

6. **`primary_key`**:
   - Specifies whether the field is the primary key for the model.
   - Automatically set to `True` for `AutoField`, `BigAutoField`, and `PrimaryKeyField` (Django 4.2+).

**Example**:- primary_key=True


7. **`unique`**:
   - Determines whether the field's values must be unique across all records in the table.
   - Set to `True` to enforce uniqueness.
   - If we try to save a model with a duplicate value in a unique field, a `django.db.IntegrityError` will be raised by the model's `save()` method.

**Example**:- unique=True


8. **`auto_created`**:
   - Used with `AutoField` to indicate that the field is automatically created by the database upon record insertion.

9. **`auto_now`**:
   - Updates the field's value to the current date and time whenever the record is updated.

10. **`auto_now_add`**:
   - Sets the field's value to the current date and time only when the record is created.

11. **`editable`**:
   - Determines whether the field can be edited in forms.
   - Set to `True` (default) to allow editing, and `False` to disable editing.

12. **`verbose_name`**:
   - Provides a human-readable name for the field, used in form labels and admin interfaces.

**Example**:- verbose_name='Student Name'

13. **`help_text`**:
   - Adds a description or help text for the field, typically displayed in forms and admin interfaces.

14. **`db_index`**:
   - Specifies whether the field should have an index in the database for improved query performance.

15. **`db_column`**:
   - Specifies the database column name for the field. By default, the field name is used as the column name.

**Example**:- db_column='Student Name'


## Built-in Field Types

Django provides a variety of built-in field types that we can use when defining our model classes. These field types correspond to various data types in a database and offer flexibility in storing and retrieving data.

Here's an overview of some commonly used built-in field types in Django:

1. **`AutoField`**:
   - Used for automatically incrementing primary keys.
   - Syntax: `models.AutoField(primary_key=True)`

2. **`BigAutoField`** (Django 3.2+):
   - Similar to `AutoField` but supports larger integer values.
   - Syntax: `models.BigAutoField(primary_key=True)`

3. **`CharField`**:
   - Used for storing short to medium-length strings.
   - Syntax: `models.CharField(max_length=<length>)`

4. **`TextField`**:
   - Used for storing longer text, such as paragraphs or descriptions.
   - Syntax: `models.TextField()`

5. **`IntegerField`**:
   - Used for storing integer values.
   - Syntax: `models.IntegerField()`

6. **`PositiveIntegerField`**:
   - Used for storing positive integer values.
   - Syntax: `models.PositiveIntegerField()`

7. **`BigIntegerField`**:
   - Used for storing larger integer values.
   - Syntax: `models.BigIntegerField()`

8. **`FloatField`**:
   - Used for storing floating-point numbers.
   - Syntax: `models.FloatField()`

9. **`DecimalField`**:
   - Used for storing decimal numbers with a specified number of decimal places.
   - Syntax: `models.DecimalField(max_digits=<total_digits>, decimal_places=<decimal_places>)`

10. **`BooleanField`**:
    - Used for storing boolean values (True or False).
    - Syntax: `models.BooleanField()`

11. **`DateField`**:
    - Used for storing dates.
    - Syntax: `models.DateField()`

12. **`TimeField`**:
    - Used for storing times.
    - Syntax: `models.TimeField()`

13. **`DateTimeField`**:
    - Used for storing both date and time.
    - Syntax: `models.DateTimeField()`

14. **`DurationField`**:
    - Used for storing a duration (time interval).
    - Syntax: `models.DurationField()`

15. **`EmailField`**:
    - Used for storing email addresses.
    - Syntax: `models.EmailField()`

16. **`ImageField`**:
    - Used for storing image files.
    - Syntax: `models.ImageField(upload_to=<upload_path>)`

17. **`FileField`**:
    - Used for storing file attachments.
    - Syntax: `models.FileField(upload_to=<upload_path>)`

18. **`URLField`**:
    - Used for storing URLs.
    - Syntax: `models.URLField()`

19. **`UUIDField`**:
    - Used for storing universally unique identifiers (UUIDs).
    - Syntax: `models.UUIDField()`

20. **`ForeignKey`**:
    - Used for creating many-to-one relationships between models.
    - Syntax: `models.ForeignKey(<related_model>, on_delete=<action>)`

21. **`OneToOneField`**:
    - Used for creating one-to-one relationships between models.
    - Syntax: `models.OneToOneField(<related_model>, on_delete=<action>)`

22. **`ManyToManyField`**:
    - Used for creating many-to-many relationships between models.
    - Syntax: `models.ManyToManyField(<related_model>)`

These are just a subset of the available field types in Django. Depending on your application's requirements, we can choose the appropriate field types to define the attributes of our models.