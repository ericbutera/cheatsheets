---
title: Query 
---

# Query Cheat Sheet
Condensed version of docs.djangoproject.com that helps me remember better.

```python
# foreign key
from blog.models import Blog, Entry
entry = Entry.objects.get(pk=1)
cheese_blog = Blog.objects.get(name="Cheddar Talk")
entry.blog = cheese_blog
entry.save()


# One-to-one relationships¶
class EntryDetail(models.Model):
    entry = models.OneToOneField(Entry, on_delete=models.CASCADE)
    details = models.TextField()

ed = EntryDetail.objects.get(id=2)
ed.entry # Returns the related Entry object.


# many to many
from blog.models import Author
joe = Author.objects.create(name="Joe")
entry.authors.add(joe)


# Many-to-many relationships
e = Entry.objects.get(id=3)
e.authors.all() # Returns all Author objects for this Entry.
e.authors.count()
e.authors.filter(name__contains='John')


a = Author.objects.get(id=5)
a.entry_set.all() # Returns all Entry objects for this Author.

b = Blog.objects.get(id=1)
b.entry_set.all() # Returns all Entry objects related to Blog.


# b.entry_set is a Manager that returns QuerySets.
b.entry_set.filter(headline__contains='Lennon')
b.entry_set.count()
```


```python
# filter chaining
(Entry.objects.filter(headline__startswith='What')
    .exclude(pub_date__gte=datetime.date.today())
    .filter(pub_date__gte=datetime.date(2005, 1, 30)))

#limit
Entry.objects.all()[:5]     # LIMIT 5
Entry.objects.all()[5:10]   # OFFSET 5 LIMIT 5
```