## Form Rendering Options


**1. `{{form}}`**

It will render all fields.

**Syntax**:
```html
<form method="get">
    {{ form}}
    <button type="submit">Submit</button>
</form>
```

**2. `{{ form.as_table }}`**

This renders the form fields as a table. Each field is placed in a separate table row.

**Syntax**:
```html
<form method="get">
    {{ form.as_table }}
    <button type="submit">Submit</button>
</form>
```

**3. `{{ form.as_p }}`**

This renders the form fields as paragraphs. Each field is wrapped in a `<p>` tag.

**Syntax**:
```html
<form method="get">
    {{ form.as_p }}
    <button type="submit">Submit</button>
</form>
```

**4. `{{ form.as_ul }}`**

This renders the form fields as an unordered list. Each field is a list item.

**Syntax**:
```html
<form method="get">
    {{ form.as_ul }}
    <button type="submit">Submit</button>
</form>
```

**5. Rendering Individual Fields**

We can also render each field individually using `{{ form.field_name }}`.

**Syntax**:
```html
<form method="get">
    {{ form.name.label_tag }} {{ form.name }}
    {{ form.email.label_tag }} {{ form.email }}
    <button type="submit">Submit</button>
</form>
```

**6. Customizing Field Output**

We can manually control the output of each field using the field's properties, such as `label_tag`, `errors`, `help_text`, and the field itself.

**Syntax**:
```html
<form method="get">
    {% csrf_token %}
    <label for="{{ form.name.id_for_label }}">Your Name:</label>
    {{ form.name }}
    {% if form.name.errors %}
        <div class="error">{{ form.name.errors }}</div>
    {% endif %}
    <small>{{ form.name.help_text }}</small>
    <button type="submit">Submit</button>
</form>
```


## Configure id attribute

**auto_id**
* The id attribute values are generated by prepending *id_* to the form field names.
* This behavior is configurable, though, if we want to change the id convention or remove HTML id attributes and <label> tags entirely.
* Use the *auto_id* argument to the Form constructor to control the id and label behavior.
* This argument must be True, False or a string. By default, *auto_id* is set to the string 'id_%s'.

**Example**:
```python
fm = StudentRegistration(auto_id=False)
fm = StudentRegistration(auto_id=True)
```

* If *auto_id* is set to a string containing the format character '%s', then the form output will include <label> tags, and will generate id attributes based on the format string.
* If *auto_id* is set to True, then the form output will include <label> tags and will use the field name as its id for each form field.
* If *auto_id* is False, then the form output will not include <label> tags nor id attributes.
* If *auto_id* is set to any other true value- such as a string that doesn't include %s- then the library will act as if *auto_id* is True.

**Benefits of Configuring id Attributes**:

**Accessibility**: Associating labels and fields improves accessibility by allowing screen readers to convey the connection between labels and inputs to users.

**Styling**: You can use CSS to style specific form fields or apply custom styling based on the id attribute.

**JavaScript Interaction**: If you need to add interactivity using JavaScript, you can target specific fields using their id attributes.


## Configure Label tag

**label_suffix**
* A translatable string (defaults to a colon (:) in English) that will be appended after any label name when a form is rendered.
* It's possible to customize that character, or omit it entirely, using the *label_suffix* parameter.
* The label suffix is added only if the last character of the label isn't a punctuation character (in English, those are ., !, ? or :)

**Syntax**
```python
fm = StudentRegistration(label_suffix="")
```


## Dynamic initial values

**initial**
* It is used to declare the initial value of form fields at runtime.
* To accomplish this, use the initial argument to a Form. This argument, if given, should be a dictionary mapping field names to initial values. Only include the fields for which we're specifying an initial value; it's not necessary to include every field in our form.
* If a Field defines initial and we include initial when instantiating the Form, then the latter initial will have precedence.


## Odering Form Field

**order_fields(field_order)**
* This method is used to rearrange the fields any time with a list of field names as in field order.
* By default `Form.field_order=None`, which retains the order in which we define the fields in our form class.
* If *field_order* is a list of field names, the fields are ordered as specified by the list and remaining fields are appended according to the default order.
* Unknown field names in the list are ignored.

**Syntax**
```python
fm=StudentRegistration()
fm.order_fields(field_order-['email', 'name'])
```