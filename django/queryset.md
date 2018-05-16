---
title: Query Set Cheat Sheet
---

# Query Set Cheat Sheet
Condensed version of docs.djangoproject.com that helps me remember better.

### [Methods returning QuerySet](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#methods-that-return-new-querysets)
```python
.filter()

.exclude(pub_date__gt=datetime.date(2005, 1, 3), headline='Hello') 
# NOT (pub_date > '2005-1-3' AND headline = 'Hello')

.order_by('-pub_date', 'headline')
.distinct()
.all()
.intersection()
.difference()
.select_related()
.prefetch_related()
```

### [Methods not returning QuerySet](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#methods-that-do-not-return-querysets)
```python
.get()
.create(first_name="Bruce", last_name="Springsteen")
obj, created = Person.objects.get_or_create(name="Butters", defaults={'nick': 'butters'})
.update_or_create()
.count()
.first()
.last()
.exists()
.delete()
.as_manager()
```


### [Field Lookups](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#field-lookups)
```python 
.get(id__exact=14)                  # id = 14
.get(id__exact=None)                # id IS NULL
                                    # iexact

.get(nick__contains='Butters')      # nick LIKE '%Lennon%'
                                    # icontains

.filter(id__in=[1, 3, 4])           # id IN (1, 3, 4)

inner_qs = Blog.objects.filter(name__contains='Cheddar')
entries = Entry.objects.filter(blog__in=inner_qs)
# SELECT ... WHERE blog.id IN (SELECT id FROM ... WHERE NAME LIKE '%Cheddar%')

.filter(id__gt=4)                   # id > 4
                                    # gte lt lte

.filter(name__startswith='Butters') # name LIKE 'Butters%'
                                    # istartswith, endswith, iendswith

start_date = datetime.date(2005, 1, 1)
end_date = datetime.date(2005, 3, 31)
Entry.objects.filter(pub_date__range=(start_date, end_date))                                  
# SELECT ... WHERE pub_date BETWEEN '2005-01-01' and '2005-03-31'

.filter(pub_date__date=datetime.date(2005, 1, 1))
.filter(pub_date__year=2005)        # pub_date BETWEEN '2005-01-01' AND '2005-12-31'
.filter(pub_date__month=12)         # EXTRACT('month' FROM pub_date) = '12'
.filter(pub_date__day=3)            # EXTRACT('day' FROM pub_date) = '3'
.filter(pub_date__week=52)           
.filter(pub_date__week__gte=32, pub_date__week__lte=38)
.filter(pub_date__week_day=2)
.filter(pub_date__time=datetime.time(14, 30))
.filter(timestamp__hour=23)         # EXTRACT('hour' FROM timestamp) = '23';
.filter(timestamp__second=31)
.filter(pub_date__isnull=True)      # pub_date IS NULL
.get(title__regex=r'^(An?|The) +')  # title REGEXP BINARY '^(An?|The) +'
.get(title__iregex=r'^(an?|the) +') # title REGEXP '^(an?|the) +'
```

### [Other](https://docs.djangoproject.com/en/1.11/ref/models/querysets/#query-related-tools)
```python
Q(question__startswith='Who') | Q(question__startswith='What')
# WHERE question LIKE 'Who%' OR question LIKE 'What%'
Q(question__startswith='Who') | ~Q(pub_date__year=2005) # NOT 2005

Poll.objects.get(
    Q(question__startswith='Who'),
    Q(pub_date=date(2005, 5, 2)) | Q(pub_date=date(2005, 5, 6))
) 
# SELECT * from polls WHERE question LIKE 'Who%'
#    AND (pub_date = '2005-05-02' OR pub_date = '2005-05-06')
```
