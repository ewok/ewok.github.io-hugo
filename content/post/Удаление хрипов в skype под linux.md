{
    "date": "2014-03-23",
    "description": null,
    "draft": false,
    "id": 16,
    "image": null,
    "meta_title": null,
    "slug": "skype-pulse",
    "tags": [
        "admins"
    ],
    "title": "Удаление хрипов в skype под linux",
    "type": "post"
}


Удаление хрипов pulseaudio в skype под linux:

	# Редактируем '/etc/pulse/default.pa'
	# меняем
	load-module module-udev-detect
	# на
	load-module module-udev-detect tsched=0

	# перезапускаем pulseaudio
	$ killall pulseaudio
	$ pulseaudio >& /dev/null &
