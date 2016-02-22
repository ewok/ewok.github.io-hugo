{
    "date": "2012-02-10",
    "description": null,
    "draft": false,
    "id": 88,
    "image": null,
    "meta_title": null,
    "slug": "tsientralnyi-pacman-kesh-dlia-domashniei-sieti",
    "tags": [
        "admins"
    ],
    "title": "Центральный pacman кэш для домашней сети",
    "type": "post"
}


Дома несколько компов с archlinux-ом. Решил я сделать, для экономии трафика, общий кэш для pacman. 

Система будет использовать sshfs и autofs.

Есть у меня слабенькая машина, которая постоянно висит онлайн. Для торрента и просто как файловое хранилище. На этой машине мы и будем держать кэш. Это сервер.

И есть два ноутбука. Это клиенты.

На всех машинах стоит arch. (Нравиться он мне :) )

На сервере нам нужен только доступ по ssh и сам каталог куда будем складывать кэш

каталог назовем к примеру "pacman_cache" и будет он находиться по пути: /mnt/pacman_cache

На клиентах ставим sshfs, autofs:

	$ pacman -S sshfs autofs

Настраиваем доступ по ssh без пароля по ключам:

rsa или dsa по выбору

	$ ssh-keygen -t dsa

На все вопросы отвечаем <Enter> 

 
Затем закидываем ключи на сервер:

	$ ssh-copy-id -i ~/.ssh/id_dsa.pub user@server

user - это пользователь имеющийся на сервере и который имеет доступ к каталогу с кэшем

server - ip нашего сервера

 После нажатия <Enter> введите пароль того самого пользователя user.

 
Если все прошло удачно, то теперь мы имеем доступ по ключам к нашему серверу. Проверяется это просто:

	$ ssh server

Настраиваем autofs:

Редактируем файл /etc/autofs/auto.master добавляем туда:
/mnt/autofs /etc/autofs/auto.mnt --timeout=30

Создаем файл /etc/autofs/auto.mnt с таким содержанием:

	pacman_cache -fstype=fuse,rw,nodev,nonempty,noatime,allow_other,max_read=65536,reconnect,uid=1000,gid=100 sshfs\#user@server\:/mnt/pacman_cache


Здесь user, server все те же пользователь и наш сервер.

Теперь нам нужно создать папку в которую все это будет автомонтироваться:

	$ mkdir /mnt/autofs


Запускаем autofs:

	$ /etc/rc.d/autofs start

 Что бы autofs поключался автоматически при загрузке системы пропишите его в /etc/rc.conf в DAEMONS

 Так, мы получили подключенный сетевой каталог в /mnt/autofs/pacman_cache

Прописываем новый путь для кэша:

Редактируем файл /etc/pacman.conf. Параметр CacheDir:

	CacheDir = /mnt/autofs/pacman_cache

Все.
