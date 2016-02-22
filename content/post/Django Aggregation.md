{
    "date": "2012-01-19",
    "description": null,
    "draft": false,
    "id": 95,
    "image": null,
    "meta_title": null,
    "slug": "django-aggregation",
    "tags": [
        "dev"
    ],
    "title": "Django Aggregation",
    "type": "post"
}


ORM это всегда баланс между производительностью и переносимостью. 

Наткнулся на очень интересную тему. Расширение функционала ORM джанги. Изучив материал, переделал и оптимизировал модели блога.

Коротко в примерах.

Есть модель:

    class Author(models.Model):
       name = models.CharField(max_length=100)
       age = models.IntegerField()
       friends = models.ManyToManyField('self', blank=True)

    class Publisher(models.Model):
       name = models.CharField(max_length=300)
       num_awards = models.IntegerField()

    class Book(models.Model):
       isbn = models.CharField(max_length=9)
       name = models.CharField(max_length=300)
       pages = models.IntegerField()
       price = models.DecimalField(max_digits=10, decimal_places=2)
       rating = models.FloatField()
       authors = models.ManyToManyField(Author)
       publisher = models.ForeignKey(Publisher)
       pubdate = models.DateField()

    class Store(models.Model):
       name = models.CharField(max_length=300)
       books = models.ManyToManyField(Book)


С ней можно делать:

    # Общее количество книг
    >>> Book.objects.count()
    2452

    # Общее количество книг с издателем BaloneyPress
    >>> Book.objects.filter(publisher__name='BaloneyPress').count()
    73

    # Средняя цена за книгу
    >>> from django.db.models import Avg
    >>> Book.objects.all().aggregate(Avg('price'))
    {'price__avg': 34.35}

    # Максимальная цена по всем книгам
    >>> from django.db.models import Max
    >>> Book.objects.all().aggregate(Max('price'))
    {'price__max': Decimal('81.20')}

    # По каждому издателю, количество книг как "num_books".
    >>> from django.db.models import Count
    >>> pubs = Publisher.objects.annotate(num_books=Count('book'))
    >>> pubs
    [<Publisher BaloneyPress>, <Publisher SalamiPress>, ...]
    >>> pubs[0].num_books
    73

    # Пятерка издателей по количеству книг.
    >>> from django.db.models import Count
    >>> pubs = Publisher.objects.annotate(num_books=Count('book')).order_by('-num_books')[:5]
    >>> pubs[0].num_books
    1323


Причем все эти методы в итоге дают QuerySet который можно фильтровать, сортировать и т.д.
