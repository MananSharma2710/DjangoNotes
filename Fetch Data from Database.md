## Fetch Data from Database

+ Writing Code to get data from database in views.py then pass it to template files using render function.
+ Get Data which is passed by render function of v`iews.py` file in template file.


- **`all()`**: Retrieves all records from the table.
- **`filter(**kwargs)`**: Retrieves records based on specified conditions.
- **`get(**kwargs)`**: Retrieves a single record based on specified conditions.

Syntax for using these methods:

```python
# Retrieve all records
all_records = MyModel.objects.all()

# Retrieve records based on conditions
filtered_records = MyModel.objects.filter(<conditions>)

# Retrieve a single record based on conditions
single_record = MyModel.objects.get(<conditions>)
```



### Writing Code to get DB data in `views.py`

+ First import our own model class from `model.py`.

**Example**
`views.py`
```python
def studentinfo(request):
    stud = Student.objects.all()
    return render(request,'student.html',{'stu':stud})
```

### Get data from `views.py` in template file

`student.html`
```html
<!DOCTYPE html>
<html>
    <body>
        <h1>Student Page</h1>
        {% if stu %}
            <h1>Show Data</h1>
            {% for st in stu%}
                <h5>{{st.stuid}}</h5>
                <h5>{{st.stuname}}</h5>
            {% endfor %}
        {% else %}
            <h1>No Data</h1>
        {% endif %}
    </body>
</html>
```
