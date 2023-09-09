## DYNAMIC URL

* A dynamic URL, also known as a parameterized URL, is a URL that includes placeholders for variables or values that can change.
* These variables are usually passed as part of the URL and are used to customize the content or behavior of a web page.

```python
urlpatterns = [
    path('student/', views.show_details, name="detail"),
    path('student/<my_id>/', views.show_details, name="detail"),
    path('student/<int:my_id>/', views.shows_details, name="detail"),
    path('student /<int:my_id>/<int:my_subid>/', views.shows_details, name="detail"),
    path('student/<int:id>/<int:subid>/<slug:my_slug>/', views.shows_details, name="detail"),
]
```

- `student/`: The static portion of the URL.
- `<int:my_id>`: A placeholder indicating an integer value that will be dynamically provided as the `my_id`.
- `views.shows_details`: The view function that will handle the request for this URL.
- `name='detail'`: A name for the URL pattern, which can be used to reverse-lookup URLs.


## Path Converters

1. **str:**
   - **Description**: Captures a string consisting of any characters except a slash (`/`).
   - **Syntax**: `str:parameter_name`
   - **Example**: `path('articles/<str:slug>/', views.article_detail)`

2. **int:**
   - **Description**: Captures an integer value.
   - **Syntax**: `int:parameter_name`
   - **Example**: `path('posts/<int:post_id>/', views.post_detail)`

3. **slug:**
   - **Description**: Captures a slug, which is a short label used in URLs (usually lowercase, with hyphens).
   - **Syntax**: `slug:parameter_name`
   - **Example**: `path('categories/<slug:category_slug>/', views.category_detail)`

4. **uuid:**
   - **Description**: Captures a universally unique identifier (UUID).
   - **Syntax**: `uuid:parameter_name`
   - **Example**: `path('items/<uuid:item_uuid>/', views.item_detail)`

5. **path:**
   - **Description**: Captures a string containing multiple path segments, including slashes.
   - **Syntax**: `path:parameter_name`
   - **Example**: `path('files/<path:file_path>/', views.file_download)`

6. **str and int combined:**
   - **Description**: Combines str and int converters to capture a mix of characters and digits.
   - **Syntax**: `str:int:parameter_name`
   - **Example**: `path('user/<str:int:username>/', views.user_profile)`