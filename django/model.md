# Models

Condensed version of docs.djangoproject.com that helps me remember better.

### Models

```python
class Test(models.Model):
  test = models.CharField(max_length=30)
```

### [Field Lookups] (https://docs.djangoproject.com/en/1.11/ref/models/querysets/#field-lookups)
exact / iexact
```python 
Thinger.objects.get(id__exact=14) SELECT ... WHERE id = 14;
Entry.objects.get(id__exact=None) SELECT ... WHERE id IS NULL
```
contains / icontains
in
gt / gte
lt / lte
startswith / istartswith
endswith / iendswith
range
date
year
month
day
week
week_day
time
hour
minute
second
isnull
search
regex
iregex
