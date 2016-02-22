{
    "date": "2012-10-23",
    "description": null,
    "draft": false,
    "id": 68,
    "image": null,
    "meta_title": null,
    "slug": "ssh-proksi",
    "tags": [
        "admins"
    ],
    "title": "ssh прокси",
    "type": "post"
}




Интересный вариант использования ssh в виде socks5 сервера.

Команда:
```
$ ssh -D <num_port> <remote_hostname>
```

запустит на локальной машине socks5 сервер с портом num_port, подключенный к remote_hostname.

Для авторизации лучше использовать ключи.
