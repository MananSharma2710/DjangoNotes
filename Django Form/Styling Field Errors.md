## FIELD ERRORS

Field errors in Django forms occur when the data entered by a user doesn't meet the validation criteria defined for a form field. These errors provide feedback to the user about what needs to be corrected.

`{{field.errors}}`
* It outputs a <ul class="errorlist"> containing any validation errors corresponding to this field.
* We can customize the presentation of the errors with a `{% for error in field.errors %}` loop.
* In this case, each object in the loop is a string containing the error message.

`{{form.non_field_errors}}` 
* This should be at the top of the form and the template lookup for errors on each field.

**Syntax to Display Field Errors in Template:**
```html
{% if form.field_name.errors %}
  <ul class="errorlist">
    {% for error in form.field_name.errors %}
      <li>{{ error }}</li>
    {% endfor %}
  </ul>
{% endif %}
```

**Example:**

```html
<form method="post" action="{% url 'submit_form' %}">
  {% csrf_token %}
  {{ form.name.label_tag }}
  {{ form.name }}
  {% if form.name.errors %}
    <ul class="errorlist">
      {% for error in form.name.errors %}
        <li>{{ error }}</li>
      {% endfor %}
    </ul>
  {% endif %}
  <button type="submit">Submit</button>
</form>
```


## Styling Django Form Errors

* If we render a bound Form object, the act of rendering will automatically run the form's validation if it hasn't already happened, and the HTML output will include the validation errors as a <ul class="errorlist"> near the field.
* We can use this class errorlist to style error.

**error_css_class** and **required_css_class** 
* These Form class hooks can be used to add class attributes to required rows or rows with errors.
* Rows will be given "error" and/or "required" classes, as needed.

**Example**:
```python
class Student Registration(forms.Form):
  error_css_class = 'error'
  required_css_class = 'required'
```
