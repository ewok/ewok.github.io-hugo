{
    "date": "2012-02-10",
    "description": null,
    "draft": false,
    "id": 89,
    "image": null,
    "meta_title": null,
    "slug": "sborka-ustanovliennogho-softa-v-pakiet-iz-arch",
    "tags": [
        "admins"
    ],
    "title": "Сборка установленного софта в пакет из arch",
    "type": "post"
}


Понадобилось мне собрать пакет из софта установленного из aur. И нашел я интересную утилиту которая делает это в два счета.

repacman называется, ставиться "йогуртом":

	$ yaourt -S repacman-en

Работает донельзя просто:

	$ repacman <имя_установленной_программы
