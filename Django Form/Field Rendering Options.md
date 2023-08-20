## Render Form Field Manually

* Each field is available as an attribute of the form using `{{form.name_of_field}}`
* `{{field.label}}` - The label of the field.

**Example**:
```html
{{form.name.label}}
```

* `{{ field.label_tag }}`- The field's label wrapped in the appropriate HTML <label> tag. This includes the form's label suffix. The default label suffix is a colon:

**Example**:
```html
{{form.name.label_tag }}
``` 

* `{{field.id_for_label}}` - The ID that will be used for this field.

**Example**:
```html
{{form.name.id_for_label}}
```

* `{{ field.value }}` - The value of the field.

**Example**: 
```html
{{form.name.value }}
```

* `{{field.html_name }}` - The name of the field that will be used in the input element's name field. This takes the form prefix into account, if it has been set.

**Example**:
```html
{{ form.name.html_name }}
``` 

* `{{field.help_text }}`- Any help text that has been associated with the field.

**Example**:
```html
{{form.name.help_text }}
``` 

`{{field.field}}` - The Field instance from the form class that this BoundField wraps. You can use it to access Field attributes.

**Example**:
```html
{{form.name.field.help_text}}
```

* `{{field.is_hidden }}`- This attribute is True if the form field is a hidden field and False otherwise. It's not particularly useful as a template variable, but could be useful in conditional tests such as:

```html
{% if field.is_hidden %}
    {# Do something special #}
{% endif %}
```
