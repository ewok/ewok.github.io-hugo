{
    "date": "2012-02-29",
    "description": null,
    "draft": false,
    "id": 82,
    "image": null,
    "meta_title": null,
    "slug": "podkliuchil-rss-v-bloghie",
    "tags": [
        "news"
    ],
    "title": "Подключил rss в блоге",
    "type": "post"
}


Подключил rss трансляцию. По джангокниге.

Самый простой вариант:

    from django.contrib.syndication.views import Feed
    from mysite.blog.models import Blog, Post

    class LatestEntriesFeed(Feed):

    title = Blog.title

    link = blog.url

    description = blog.description

    def items(self):

    return Post.objects.filter(draft=False)[:10]

    def item_title(self, item):

    return item.title

    def item_description(self, item):

    # Здесь попытка подключить lj-cut, для кросспостинга в ЖЖ. Посмотрим, сработает или нет.

    return item.entry.replace(u'<!-- pagebreak -->', u'<lj-cut text="Читать полностью">')

    def item_pubdate(self, item):

    return item.date

    def item_categories(self, item):

    return item.tag.all()

 

+ Прописать в urls.py:

        from mysite.blog.feeds import LatestEntriesFeed
        urlpatterns = patterns('',
        url(r'^rss$', LatestEntriesFeed()),
        )

Единственный косяк. Почему-то в тэге 'description' html идет с эскейпами. Пока что не получилось это исправить.
