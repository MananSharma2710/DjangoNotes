## TEMPLATE INHERITANCE/EXTENDING

+ Template inheritance is a powerful feature in Django's template system that allows us to create a base template with a consistent structure and then extend and override specific content blocks in child templates.
+ This approach enables us to maintain a consistent layout across multiple pages while customizing the content of each page as needed.
+ The *extends* tag is used to inherit template.
+ *extends* tag tells the template engine that this template *extends* another template.
+ When the template system evaluates this template, first it locates the parent let's assume, `base.html`.
+ At that point, the template engine will notice the block tags in `base.html` and replace those blocks with the contents of the child template.
+ We can use as many levels of inheritance as needed.


### How template inheritance works

1. **Base Template (Parent Template)**:
   + The base template defines the overall structure of our pages.
   + It includes the common elements such as the header, navigation menu, and footer.
   + However, it leaves certain content areas (known as "blocks") empty, allowing child templates to provide specific content for those areas.

   ```html
   <!-- base.html -->
   <!DOCTYPE html>
   <html>
   <head>
       <title>{% block title %}Default Title{% endblock %}</title>
   </head>
   <body>
       <header>
           <!-- Common header content -->
       </header>
       <nav>
           <!-- Common navigation menu -->
       </nav>
       <main>
           {% block content %}{% endblock %}
       </main>
       <footer>
           <!-- Common footer content -->
       </footer>
   </body>
   </html>
   ```

2. **Child Templates**:
   + Child templates extend the base template and provide content for the blocks defined in the base template.
   + Child templates only need to specify the content for the blocks they want to override, leaving the rest of the layout intact.

   ```html
   <!-- page1.html -->
   {% extends "base.html" %}
   {% block title %}Page 1{% endblock %}
   {% block content %}
       <h1>Welcome to Page 1</h1>
       <p>This is the content for Page 1.</p>
   {% endblock %}

   <!-- page2.html -->
   {% extends "base.html" %}
   {% block title %}Page 2{% endblock %}
   {% block content %}
       <h1>Welcome to Page 2</h1>
       <p>This is the content for Page 2.</p>
   {% endblock %}
   ```

3. **Inheritance in Action**:
   + When we render a child template, Django processes the `extends` tag and locates the corresponding blocks in the base template.
   + It replaces the block content in the base template with the content specified in the child template.

   For example, rendering `page1.html` based on the `base.html` layout would result in a page with the title "Page 1" the common header and footer, and the specific content for Page 1.


## `{% extends %}` Tag

+ The *extends* tag is used to inherit template. It tells the template engine that this template "extends" another template. It has no end tag.

**Syntax**

```html
{% extends 'parent_template_name' %}

{% extends variable %}
```

**Example**

```html
{% extends "./basel.html" %}

{% extends "../base2.html" %}

{% extends "/my/base3.html" %}

{% extends something %}
```


## `{% block %}` Tag

+ The *block* tag is used to for overridding specific part of a template.

**Syntax**

```html
{% block blockname %}.... {% endblock %}

{% block blockname %}.... {% endblock blockname %}
```

**Example**

```html
{% block title %} {% endblock %}

{% block content %}..... {% endblock content %}
```


## RULES

+ If We use `{% extends %}` in a template, it must be the first template tag in that template. Template inheritance won't work, otherwise.
+ More `{% block %}` tags in our base templates are better.
+ Child templates don't have to define all parent blocks, so we can fill in reasonable defaults in a number of blocks, then only define the ones we need later.
+ We Can't define multiple block tags with the same name in the same template.
+ If We need to get the content of the block from the parent template, the `{{block.super}}` variable will do the trick.

