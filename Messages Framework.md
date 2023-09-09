## Messages Framework

* The messages framework allows us to temporarily store messages in one request and retrieve them for display in a subsequent request.
* Django provides full support for cookie- and session-based messaging, for both anonymous and authenticated users.

```python
INSTALLED APPS = ['django.contrib.messages']
```

```python
MIDDLEWARE = [
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware']
```

```python
'context_processors': ['django.contrib.messages.context_processors.messages']
```

## Message Level and Tag

* The messages framework is based on a configurable level architecture similar to that of the Python logging module.

**Message Level** – Message levels allow you to group messages by type so they can be filtered or displayed differently in views and templates.

**Message Tag** - Message tags are a string representation of the message level plus any extra tags that were added directly in the view. Tags are stored in a string and are separated by spaces. Typically, message tags are used as CSS classes to customize message style based on message type.

|  Level        | Tag        | Value         | Purpose                                         |
|---------------|------------|---------------|-------------------------------------------------|
| DEBUG         | debug      | 10            | Development related messages that will be ignored or removed in a production deployment       |
| INFO          | info       | 20            | Informational messages for the user      |
| SUCCESS       | success    | 25            | An action was successful, e.g. "Updated Successfully"      |
| WARNING       | warning    | 30            | A failure did not occur but may be imminent                  |
| ERROR         | error      | 40            | An action was not successful or some other failure occurred       |

## How to use

**Write Messages**
`add_message(request, level, message, extra_tags=", fail_silently=False)` - This method is used to add/write messages.

`fail_silently = True` only hides the MessageFailure that would otherwise occur when the messages framework disabled and one attempts to use one of the add_message family of methods. It does not hide failures that may occur for other reasons.

```python
from django.contrib import messages
messages.add_message(request, messages.INFO, 'Message')
```

**Write Message by Shortcut Methods**
```python
from django.contrib import messages
messages.debug(request, '%s SQL statements were executed', %count)
messages.info(request, 'two credits in account')
messages.success(request, 'Updated')
messages.warning(request, 'Expiring in 2 days')
messages.error(request, 'Deleted')
```

**Display Message**
```python
{% if messages %}
    {% for message in messages %}
        {% if message.tags %}
            {{message.tags}}
        {% endif %}
        {{message}}
    {% endfor %}
{% endif %}
```

## Methods

`get_level()`- This method is used to retrieved the current effective level.
```python
from django.contrib import messages
current_level = messages.get_level(request)
```


`set_level()`- This method is used to set minimum recorded level.
```python
from django.contrib import messages
messages.set_level(request, messages.DEBUG)
```
This will record messages with a level of DEBUG and higher.

## Change Tags

Open *settings.py*
```python
from django.contrib import messages import constants as messages
MESSAGE_TAGS = {
    messages.ERROR:'danger'
}
```