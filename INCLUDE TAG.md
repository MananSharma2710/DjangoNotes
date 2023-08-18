## INCLUDE TAG

+ It is used to include the contents of another template file within the current template.
+ This allows us to reuse and modularize sections of our templates, promoting code reusability and maintainability.
+ Each *include* is a completely independent rendering process.
+ The template name can either be a variable or a hard-coded (quotes) string, in either single or double quotes.
+ We can pass additional context explicitly to the template using *with* keyword.

**Syntax**

```html
<!-- Method 1 -->
{% include temp_var_name %}

<!-- Method 2 -->
{% include "template_name.html" %}

<!-- Method 3 -->
{% include "folder/template_name.html" %}

<!-- Method 4 using with keyword -->
{% include "template_name.html" with variable_name=value %}

<!-- Method 4 using with and only keyword -->
{% include "template_name.html" with variable_name=variable_value only %}


```


Here's how the `{% include ... %}` template tag works:

```html
{% include "template_name.html" %}

{% include "template_name.html" with variable_name=value %}

{% include "template_name.html" with variable_name=variable_value only %}

```

- `{% include ... %}`:
    + This is the template tag used to include the contents of another template.

- `"template_name.html"`:
    + Replace this with the path to the template file we want to include.
    + The path should be specified relative to the `templates` directory.

- `variable_name=value`:
    + This is where we specify the additional context variable(s) we want to pass to the included template.
    + `variable_name` is the name of the variable that will be available in the included template, and value is the value we want to assign to that variable.

- `only`:
    + This keyword restricts the context variables available in the included template to only those explicitly provided in the with part of the tag.
    + No other variables are available to the included template.

Here's an example:

Assuming you have a reusable template named `sidebar.html`
and `product.html` that we want to include in multiple pages:

```html
<!-- sidebar.html -->
<div class="sidebar">
    <!-- Sidebar content -->
</div>

<!-- product.html -->
<div class="product">
    <h2>{{ product_name }}</h2>
    <p>{{ description }}</p>
</div>

```

In our main template, we can use the `{% include ... %}` template tag to include the `sidebar.html` template:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Website</title>
</head>
<body>
    <header>
        <!-- Header content -->
    </header>

    <main>
        <!-- Main content -->
    </main>

    {% include "sidebar.html" %}

    {% include "product.html" with product_name="Widget" description="A fantastic widget." %}
    <footer>
        <!-- Footer content -->
    </footer>
</body>
</html>
```

When the template is rendered, the contents of `sidebar.html` and `product.html` will be included in the main template, and the `product_name` and `description` context variables will be available within the included template.. This allows us to reuse the files across different pages without duplicating the same HTML code.

Using the `{% include ... %}` template tag enhances code organization and reusability by enabling you to modularize our templates and keep them clean and maintainable.

Using the `{% include ... with ... %}` template tag with the 'with' keyword allows us to pass custom context variables to included templates, providing flexibility and reusability in your templates.