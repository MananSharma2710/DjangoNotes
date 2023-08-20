## ORM 

+ **Object-Relational Mapper (ORM)**, which enables application to interact with database such as SQLite, MySQL, PostgreSQL, Oracle.
+ ORMS automatically create a database schema from defined classes or models.
+ It generate SQL from Python code for a particular database which means developer do not need to write SQL Code.
+ ORM maps objects attributes to respective table fields.
+ It is easier to change the database if we use ORMS hence project becomes more portable.
+ Django's ORM is just a way to create SQL to query and manipulate your database and get results in a pythonic fashion.
+ ORMS use connectors to connect databases with a web application.


## How ORM works:

1. **Mapping Entities to Tables**:
    + In an ORM system, we define classes (entities) that represent the tables in our database.
    + Each attribute of the class corresponds to a column in the table.
    + Relationships between tables are represented as object references within the classes.

2. **Creating and Querying Objects**:
    + With ORM, we create instances of these classes to represent rows in the database.
    + We can manipulate these objects using the programming language's features and methods.
    + For example, we can create, update, and delete records using methods provided by the ORM library.

3. **Automatic SQL Generation**:
    + When we perform operations on ORM objects (such as saving an object to the database), the ORM library generates the necessary SQL statements (INSERT, UPDATE, DELETE, etc.) behind the scenes.
    + This relieves us from writing explicit SQL queries.

4. **Abstraction of Database Details**:
    + ORM shields developers from dealing with low-level database details, like connection management, query optimization, and data conversion.
    + We can work with high-level concepts and use a consistent API provided by the ORM library.

5. **Portability**:
    + ORM libraries often abstract database-specific syntax differences.
    + This means that we can write our code in a way that is compatible with different database systems without major modifications.

6. **Data Validation and Type Safety**:
    + ORM systems often provide features for data validation and type safety.
    + This ensures that the data we're working with meets certain criteria and adheres to a consistent data structure.

7. **Querying the Database**:
    + ORM libraries provide ways to query the database using an object-oriented syntax.
    + We can retrieve data by filtering, ordering, and joining objects, which the ORM translates into SQL queries.

8. **Migrations and Schema Management**:
    + Many ORM systems offer features to handle database schema changes over time.
    + This includes creating, altering, and deleting tables as your application's data model evolves.


## QUERYSET

+ It is a powerful tool that represents a collection of database queries that can be executed against a database to retrieve, filter, and manipulate data.
+ It allow us to read the data from the database, filter and order it.
+ It allow us to interact with our database using a high-level, Pythonic API, abstracting away much of the complexity of writing raw SQL queries.

Here's an explanation of key concepts related to QuerySets:

1. **Retrieving Objects**:
    + QuerySets are used to retrieve objects (rows) from a database table (model).
    + We can retrieve all objects of a certain type or filter objects based on specific conditions.

2. **Lazy Evaluation**:
    + QuerySets use lazy evaluation.
    + This means that the actual database query is not executed until we explicitly request the data or perform an action that requires database access, such as iterating over the QuerySet or evaluating its length.

3. **Chaining Filters and Methods**:
    + We can chain multiple filters and methods together to build complex queries.
    + Each method we chain narrows down the result set further.

4. **Methods and Operations**:
    + QuerySets provide a wide range of methods and operations to query and manipulate data, including:
        - `filter()`: Retrieve objects that meet certain criteria.
        - `exclude()`: Retrieve objects that do not meet certain criteria.
        - `annotate()`: Add calculated fields to the results.
        - `order_by()`: Order the results based on one or more fields.
        - `distinct()`: Retrieve unique results.
        - `aggregate()`: Perform aggregate calculations (e.g., sum, average) on the results.
        - `count()`: Get the count of objects that match the QuerySet.
        - `exists()`: Check if any objects match the QuerySet.
        - `values()`, `values_list()`: Retrieve specific fields as dictionaries or tuples.
        - `get()`: Retrieve a single object that matches the query (raises an exception if not found).

5. **Evaluating a QuerySet**:
    + To retrieve the actual data from a QuerySet, we can evaluate it using methods like `list()`, `get()`, `first()`, or by iterating over it. This is when the database query is executed.

6. **Caching**:
    + QuerySets can be cached to avoid repeated database queries when the same data is requested multiple times within the same session.

7. **Relationships and Joins**:
    + QuerySets can navigate and follow relationships defined in models.
    + For example, we can retrieve all related objects using a ForeignKey or reverse ForeignKey relationship.

Here's an example of using QuerySets in Django:

```python
from myapp.models import Book

# Retrieve all books published after 2000
recent_books = Book.objects.filter(publication_date__gt='2000-01-01')

# Order the books by publication date
ordered_books = recent_books.order_by('-publication_date')

# Retrieve the first book in the ordered QuerySet
first_book = ordered_books.first()

# Count the number of books in the QuerySet
book_count = ordered_books.count()

# Check if any books match the QuerySet
has_books = ordered_books.exists()

# Get a list of dictionaries with selected fields
selected_fields = ordered_books.values('title', 'author')

# Iterate over the QuerySet and print book titles
for book in ordered_books:
    print(book.title)
```

QuerySets provide a powerful and flexible way to interact with our database using a high-level API, helping we write efficient and maintainable code while avoiding the need to write raw SQL queries.