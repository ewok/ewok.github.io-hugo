{
    "date": "2014-12-08",
    "description": null,
    "draft": false,
    "id": 9,
    "image": null,
    "meta_title": null,
    "slug": "file-too-large-qcow2-file",
    "tags": [
        "admins"
    ],
    "title": "File too large. Qcow2 file.",
    "type": "post"
}


Если испортился при работе с qcow через qemu-img у вас вылезла ошибка "File too large". То вытащить данные можно таким способом. Качаем исходники qemu версии 1.7.2. Разархивируем и делаем "./configure && make". То есть БЕЗ установки. Далее забираем файл qemu-img и используем его для конвертации в raw.

`./qemu-img convert -f qcow2 -O raw откуда куда`

В принципе с этого момента данные уже можно восстановить, примонтировав образ диска.
