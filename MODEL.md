## MODEL 

* It is the single, definitive source of information about our data.
* It contains the essential fields and behaviors of the data we're storing.
* Generally, each model maps to a single database base.

* It is a Python class that defines the structure and behavior of a database table.
* It's a core component of Django's Object-Relational Mapping (ORM) system, which allows us to work with databases using Python objects and methods rather than raw SQL queries.


## MODEL CLASS

* Model class is a class which will represent a table in database.
* Each model is a Python class that subclasses `django.db.models.Model`.
* Each attribute of the model represents a database field.
* With all of this, Django gives us an automatically-generated database-access API Django provides built-in database by default that is sqlite database.
* We can use other database like MySQL, Oracle SQL etc.


## Key points:

1. **Data Structure Definition**:
    + A Model class defines the fields and their data types that will be stored in a database table.
    + Each attribute of the class represents a column in the table.

2. **Database Interaction**:
    + Models abstract the interaction with the database.
    + We can create, retrieve, update, and delete records in the database using instances of Model classes.

3. **ORM Mapping**:
    + The ORM maps Model classes to database tables, automatically generating SQL queries for us based on the Python code we write.

4. **Fields and Attributes**:
    + Fields in a Model class correspond to columns in the database table.
    + Each field specifies the data type and can have additional attributes like maximum length, default values, and more.

5. **Relationships**:
    + Models can define relationships between each other, such as ForeignKey (many-to-one), OneToOneField, and ManyToManyField.
    + These relationships help organize and connect data in our application.

6. **Validation**:
    + Models provide built-in data validation.
    + We can specify constraints on fields to ensure data integrity before it's saved to the database.

7. **Admin Interface**:
    + Django's admin interface automatically generates forms for creating and editing records based on the Model's fields.

8. **Migrations**:
    + Models are used to generate database schema migrations.
    + These migrations define changes to the database structure as our application evolves.

9. **Model Methods**:
    + We can define methods on our Model classes to encapsulate business logic related to the data they represent.

10. **Custom Managers**:
    + Models can define custom managers to encapsulate query logic and provide reusable methods for data retrieval.

11. **Reusable Templates**:
    + Model classes can be instantiated to create objects that adhere to the defined data structure.
    + This promotes code reusability and consistency throughout our application.

Example of a simple Django Model:

```python
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.CharField(max_length=100)
    publication_date = models.DateField()

    def __str__(self):
        return self.title
```

In this example, the `Book` Model represents a database table with three columns: `title`, `author`, and `publication_date`. Using this Model, we can interact with the database, create records, perform queries, and more, all using Python code without writing raw SQL queries.


## CREATE OUR OWN MODEL CLASS

+ `models.py` file which is inside application folder, is required to create our own model'tlass.
+ Our own model class will inherit Python's Model Class.

**Syntax**

```python
class ClassName(models.Model):
    field name models.FieldType(arg, options)
```

**Example**

```python
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.CharField(max_length=100)
    publication_date = models.DateField()
```

* This class will create a table with columns and their data types.
* Table Name will be *ApplicationName_ClassName*, in this case it will be *Book*.
* Field name will become table's Column Name, in this case it will be title, author, publication_date with their data type.
* As we have not mentioned primary key in any of these columns so it will automatically create a new column named 'id' as Type Integer with primary key and auto increment.


## RULES

* Field Name instantiated as a class attribute and represents a particular table's Column name.
* Field Type is also known as Data Type.
* A field name cannot be a Python reserved word, because that would result in a Python syntax error.
* A field name cannot contain more than one underscore in a row, due to the way Django's query lookup syntax works.
* A field name cannot end with an underscore.


## How to use Models

* Once we have defined our models, we need to tell Django we're going to use those models.
* **Run Migrations**
Run the following commands to create and apply the initial migrations:

```bash
python manage.py makemigrations
python manage.py migrate
```


## Model Operations

