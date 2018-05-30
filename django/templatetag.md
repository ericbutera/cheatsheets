---
title: Template Tags
---

# Template Tags and Filters

## [Template Tags](https://docs.djangoproject.com/en/1.11/howto/custom-template-tags/)

### [Simple Tags](https://docs.djangoproject.com/en/1.11/howto/custom-template-tags/#simple-tags)

Easy way to include partials

```python
# ./extrasapp/templatetags/timeexample_tags.py
import datetime
from django import template

register = template.Library()

@register.simple_tag
def current_time(format_string):
    return datetime.datetime.now().strftime(format_string)
```
```htmldjango
{% load timeexample %}
{% current_time "%Y-%m-%d %I:%M %p" as the_time %}
<p>The time is {{ the_time }}.</p>
```

### [Inclusion Tags](https://docs.djangoproject.com/en/1.11/howto/custom-template-tags/#inclusion-tags)
```python
from django import template

register = template.Library()

@register.inclusion_tag(takes_context=True, filename='path/to/partial.html')
def jump_link(context):
    return {
        'link': context['home_link'],
        'title': context['home_title'],
    }

```
```htmldjango
<!-- path/to/partial.html -->
Jump directly to <a href="{{ link }}">{{ title }}</a>.

<!-- usage in template -->
{% jump_link %}
```

### [Assignment Tags](https://docs.djangoproject.com/en/1.11/howto/custom-template-tags/#assignment-tags)

Allows tag to be stored in a variable instead of directly rendered. Useful for conditionals

```python
@register.assignment_tag
def get_current_time(format_string):
    return datetime.datetime.now().strftime(format_string)
```
```htmldjango
{% get_current_time "%Y-%m-%d %I:%M %p" as the_time %}
<p>The time is {{ the_time }}.</p>
```

### [Filters](https://docs.djangoproject.com/en/1.11/howto/custom-template-tags/#writing-custom-template-filters)
 
```python
from django import template

register = template.Library()

@register.filter(name='cut')
def cut(value, arg):
    """Removes all values of arg from the given string"""
    return value.replace(arg, '')
```

```htmldjango
{{ somevariable|cut:"0" }}
```
