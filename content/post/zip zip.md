{
    "date": "2012-10-14",
    "description": null,
    "draft": false,
    "id": 70,
    "image": null,
    "meta_title": null,
    "slug": "zip-zip",
    "tags": [
        "dev"
    ],
    "title": "zip zip",
    "type": "post"
}


Прикольный пример из книги Лутца("Изучаем Python").

 

    >>> X = (1, 2)

    >>> Y = (3, 4)

    >>> A, B = zip(*zip(X, Y))

    >>> A

    (1, 2)

    >>> B

    (3, 4)

 

Распаковываем запакованные кортежи запаковыванием. 
