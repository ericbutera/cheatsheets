---
title: Fields
---

# [Fields](https://docs.djangoproject.com/en/1.11/ref/forms/fields/)

## Core Field Args

```python
Field(required=True)
Field(label="Human Friendly Name")
Field(label_suffix="?") # Age?
Field(initial="Your name")
Field(widget=Widget Class)
Field(help_text="Descriptive text for field")
Field(label="name", error_messages={'required':"Please enter your name"})
Field(validators=...) # https://docs.djangoproject.com/en/1.11/ref/validators/
Field(disabled=False)
```

## Field Classes

```python
BooleanField(**kwargs) # widget=CheckboxInput
CharField(min_length=, max_length=, strip=, empty_value=, **kwargs) # widget=TextInput
ChoiceField(**kwargs) # widget=ChoiceField
TypedChoiceField(coerce=, empty_value=, **kwargs) # widget=ChoiceField
DateField(input_formats=['%Y-%m-%d'], **kwargs) # widget=DateInput
DateTimeField(input_formats=, **kwargs) # widget=DateTimeInput
DecimalField(max_value=, min_value=, max_digits=, decimal_places=, **kwargs) # widget=NumberInput|TextInput
DurationField(**kwargs)
EmailField(max_length=, min_length=,**kwargs) # widget=EmailInput
FileField(max_length=, **kwargs) # widget=ClearableFileInput
FilePathField(path=, recursive=, match=, allow_files=, allow_folders=) # widget=Select
FloatField(max_value=, min_value=, **kwargs) # widget=NumberInput|TextInput
ImageField(**kwargs) # ClearableFileInput
IntegerField(max_value=, min_value=, **kwargs) # NumberInput|TextInput
MultipleChoiceField(**kwargs) # widget=SelectMultiple
TypedMultiChoiceField(**kwargs)
NullBooleanField(**kwargs) # NullBooleanField
RegexField(regex=, strip=, max_length=, min_length=, **kwargs) # widget=TextInput
SlugField(allow_unicode=, **kwargs) # widget=TextInput
TimeField(input_formats='%H:%M', **kwargs) # widget=TextInput
URLField(max_length=, min_length=, **kwargs) # widget=URLInput

ComboField()
MultiValueField()
SplitDateTimeField()
ModelChoiceField(queryset=, empty_label=, to_field_name=, **kwargs)
ModelMultipleChoiceField()
```
