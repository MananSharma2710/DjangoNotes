## Model Operations

In Django's migrations, model operations define the changes you want to make to your database schema. These operations are represented as objects within a migration's `operations` list. Here are some common model operations along with their syntax:

1. **Creating a Model**:
   - Operation: `migrations.CreateModel`
   - Syntax:
     ```python
     migrations.CreateModel(
         name='<ModelName>',
         fields=[
             ('<field_name>', models.<FieldType>(<options>)),
             # ...
         ],
         options=None,
         bases=None,
         managers=None
     )
     ```
Where,

+ *name* is the model name, as would be written in the `models.py` file.
+ *fields* is a list of 2-tuples of `(field_name, field_instance)`. The field instance should be an unbound field (so just models.CharField(...), rather than a field taken from another model).
+ *options* is an optional dictionary of values from the model's Meta class.
+ *bases* is an optional list of other classes to have this model inherit from; it can contain both class objects as well as strings in the format "appname.ModelName" if we want to depend on another model (so you inherit from the historical version). If it's not supplied, it defaults to inheriting from the standard models.Model.
+ *managers* takes a list of 2-tuples of `(manager_name, manager instance)`. The first manager in the list will be the default manager for this model during migrations

2. **Adding a Field**:
   - Operation: `migrations.AddField`
   - Syntax:
     ```python
     migrations.AddField(
         model_name='<ModelName>',
         name='<field_name>',
         field=models.<FieldType>(<options>),
     )
     ```

3. **Altering a Field**:
   - Operation: `migrations.AlterField`
   - Syntax:
     ```python
     migrations.AlterField(
         model_name='<ModelName>',
         name='<field_name>',
         field=models.<FieldType>(<options>),
     )
     ```

4. **Altering Model Table**
    - Operation: `migrations.AlterModelTable`
    - Syntax:
     ```python
     migrations.AlterModelTable(
    name='<ModelName>',
    table='<new_table_name>',
    )
     ```

5. **Renaming a Field**:
   - Operation: `migrations.RenameField`
   - Syntax:
     ```python
     migrations.RenameField(
         model_name='<ModelName>',
         old_name='<old_field_name>',
         new_name='<new_field_name>',
     )
     ```

6. **Removing a Field**:
   - Operation: `migrations.RemoveField`
   - Syntax:
     ```python
     migrations.RemoveField(
         model_name='<ModelName>',
         name='<field_name>',
     )
     ```

7. **Deleting a Model**:
   - Operation: `migrations.DeleteModel`
   - Syntax:
     ```python
     migrations.DeleteModel(
         name='<ModelName>',
     )
     ```

8. **Adding an Index**:
   - Operation: `migrations.AddIndex`
   - Syntax:
     ```python
     migrations.AddIndex(
         model_name='<ModelName>',
         index=models.Index(fields=['<field_name>']),
     )
     ```

9. **Adding Unique Constraint**:
   - Operation: `migrations.AddConstraint`
   - Syntax:
     ```python
     migrations.AddConstraint(
         model_name='<ModelName>',
         constraint=models.UniqueConstraint(fields=['<field_name>'], name='<constraint_name>'),
     )
     ```

10. **Adding Check Constraint**:
   - Operation: `migrations.AddConstraint`
   - Syntax:
     ```python
     migrations.AddConstraint(
         model_name='<ModelName>',
         constraint=models.CheckConstraint(check='<check_condition>', name='<constraint_name>'),
     )
     ```

11. **Adding Foreign Key Constraint**:
    - Operation: `migrations.AddConstraint`
    - Syntax:
      ```python
      migrations.AddConstraint(
          model_name='<ModelName>',
          constraint=models.ForeignKey(
              '<related_model>',
              '<field_name>',
              on_delete=models.<Action>,
          ),
      )
      ```

12. **Custom SQL Operation**:
    - Operation: `migrations.RunSQL`
    - Syntax:
      ```python
      migrations.RunSQL(
          '<SQL_statement>',
          '<SQL_statement>',
          # ...
      )
      ```

These are just a few examples of model operations that you can use in Django migrations. The actual syntax and options might vary based on your specific use case and the changes you want to make to your database schema.