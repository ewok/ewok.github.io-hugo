{
    "date": "2012-11-14",
    "description": null,
    "draft": false,
    "id": 63,
    "image": null,
    "meta_title": null,
    "slug": "django-filebrowser-no-grappelli-tinymce",
    "tags": [
        "dev"
    ],
    "title": "django-filebrowser-no-grappelli + tinymce",
    "type": "post"
}


Настройка, уже вполне популярной связки django-filebrowser-no-grappelli + tinymce.

Настройку я производил по инструкции из гугла:

* Урлы:
	url(r'^tinymce/filebrowser/',include('filebrowser.urls'))
* settings:
INSTALLED_APPS = (..., 'filebrowser',)
FILEBROWSER_DIRECTORY = 'upload/'

Но! Настройка не шла. 
Оказывается по умолчанию django-filebrowser за основу путей берет MEDIA_ROOT и MEDIA_URL, что вполне логично!
А так как я ими не пользовался, все у меня было по STATIC_ROOT и STATIC_URL, то у меня вылазили ошибки. 
 
Нужно указать:
 
	FILEBROWSER_MEDIA_ROOT = STATIC_ROOT
	FILEBROWSER_MEDIA_URL = STATIC_URL
 
После чего у меня все заработало как должно.
