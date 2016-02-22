{
    "date": "2015-03-19",
    "description": null,
    "draft": false,
    "id": 6,
    "image": null,
    "meta_title": null,
    "slug": "iesli-pieriestal-obnovliatsia-fail-resolv-conf-na-mint",
    "tags": [
        "admins"
    ],
    "title": "Если перестал обновляться файл resolv.conf на mint",
    "type": "post"
}


Можно попробовать так:

`sudo dpkg-reconfigure resolvconf`

Или так:

	sudo mv /etc/resolv.conf /run/resolvconf/resolv.conf
	sudo ln -s /run/resolvconf/resolv.conf /etc/resolv.conf

Мне помог второй способ.

Еще вариант:

	В /etc/NetworkManager/NetworkManager.conf закомментируйте dns=dnsmasq
	sudo dpkg-reconfigure resolvconf 
	sudo resolvconf --enable-updates 
