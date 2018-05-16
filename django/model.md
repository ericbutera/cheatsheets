---
title: Models
---

# [Models](https://docs.djangoproject.com/en/1.11/topics/db/models/)
Condensed version of docs.djangoproject.com that helps me remember better.

### Definition

```python
class Test(models.Model):
  test = models.CharField(max_length=30)
```


# [Fields](https://docs.djangoproject.com/en/1.11/ref/models/fields/)

### [Field Options](https://docs.djangoproject.com/en/1.11/ref/models/fields/#field-options)
```python
Field(null=True)        # store empty values as NULL in the database
Field(blank=True)       # allowed to be blank (code validation only)
Field(db_column='name') # name of the database column to use'
Field(db_index=True)    # create index on field?
Field(default='value')  # default value of field
Field(editable=False)   # hide from admin or any ModelForm, skip validation
Field(help_text='Field Documentation')
Field(primary_key=True) # use this to specific custom pk field
Field(unique=True)      # unique value
Field(verbose_name='')  # human readable name for field

FRESHMAN = 'FR'
SOPHOMORE = 'SO'
JUNIOR = 'JR'
SENIOR = 'SR'
YEAR_IN_SCHOOL_CHOICES = (
    (FRESHMAN, 'Freshman'),
    (SOPHOMORE, 'Sophomore'),
    (JUNIOR, 'Junior'),
    (SENIOR, 'Senior'),
)
.CharField(max_length=2, choices=YEAR_IN_SCHOOL_CHOICES, default=FRESHMAN,)
```

### [Field Types](https://docs.djangoproject.com/en/1.11/ref/models/fields/#field-types)
```python
AutoField()
BigAutoField()
BigIntegerField()
BinaryField()
BooleanField()
CharField(max_length=None, ...)
CommaSeparatedIntegerField(max_length=None, ...)
DateField(auto_now=False, auto_now_add=False, ...)
DateTimeField(auto_now=False, auto_now_add=False, ...)
DecimalField(max_digits=None, decimal_places=None,  ...)
DurationField()
EmailField(max_length=254, ...)
FileField(upload_to=None, max_length=100, ...)  # returns FieldFile()
  FieldFile.name
  FieldFile.size
  FieldFile.url
  FieldFile.delete(save=True)
FilePathField(path=None, match=None, recursive=False, max_length=100, ...)
FloatField()
ImageField(upload_to=None, height_field=None, width_field=None, max_length=100, ...)
IntegerField()
GenericIPAddressField(protocol='both', unpack_ipv4=False, ...)
NullBooleanField()
PositiveIntegerField()
PositiveSmallIntegerField()
SlugField(max_length=50, ...)
SmallIntegerField()
TextField()
TimeField(auto_now=False, auto_now_add=False, ...)
URLField(max_length=200, ...)
UUIDField()
```

### [Relationships](https://docs.djangoproject.com/en/1.11/topics/db/models/#relationships)

#### [Many-to-one relationships](https://docs.djangoproject.com/en/1.11/topics/db/models/#many-to-one-relationships)
```python
class Manufacturer(models.Model):
    pass

class Car(models.Model):
    manufacturer = models.ForeignKey(Manufacturer, on_delete=models.CASCADE)
```

#### [Many-to-many relationships](https://docs.djangoproject.com/en/1.11/topics/db/models/#many-to-many-relationships)
```python
 Topping(models.Model):
    pass

class Pizza(models.Model):
    toppings = models.ManyToManyField(Topping)
```

#### [Extra fields on many-to-many relationships](https://docs.djangoproject.com/en/1.11/topics/db/models/#extra-fields-on-many-to-many-relationships)
```python
class Person(models.Model):
    name = models.CharField(max_length=128)

class Group(models.Model):
    name = models.CharField(max_length=128)
    members = models.ManyToManyField(Person, through='Membership')

class Membership(models.Model):
    person = models.ForeignKey(Person, on_delete=models.CASCADE)
    group = models.ForeignKey(Group, on_delete=models.CASCADE)
    date_joined = models.DateField()
    invite_reason = models.CharField(max_length=64)
```

### [Meta](https://docs.djangoproject.com/en/1.11/topics/db/models/#meta-options)
```python
class Ox(models.Model):
    horn_length = models.IntegerField()

    class Meta:
        ordering = ["horn_length"]
        verbose_name_plural = "oxen"


# Meta inheritance
class CommonInfo(models.Model):
    class Meta:
        abstract = True
        ordering = ['name']

class Student(CommonInfo):
    class Meta(CommonInfo.Meta):
        db_table = 'student_info'
```


### Examples
```python
class Blog(models.Model):
    name = models.CharField(max_length=100)
    tagline = models.TextField()

class Author(models.Model):
    name = models.CharField(max_length=200)
    email = models.EmailField()

class Entry(models.Model):
    blog = models.ForeignKey(Blog, on_delete=models.CASCADE)
    headline = models.CharField(max_length=255)
    body_text = models.TextField()
    pub_date = models.DateField()
    mod_date = models.DateField()
    authors = models.ManyToManyField(Author)
    n_comments = models.IntegerField()
    n_pingbacks = models.IntegerField()
    rating = models.IntegerField()

```