{
    "date": "2015-04-02",
    "description": null,
    "draft": false,
    "id": 116,
    "image": "/images/2015/04/kvmbanner-logo2.png",
    "meta_title": null,
    "slug": "virsh-polieznyie-kommandy",
    "tags": [
        "admins"
    ],
    "title": "libvirt - полезные комманды",
    "type": "post"
}


# Установка
Debian/ubuntu и производные:
		
        apt-get instll libvirt-bin -y
        
На rhel подобных что-то типа:

		yum install libvirt-client -y
        
# virsh
Консоль для управления виртуальным окружением<br>
Подключение: `virsh --connect=<строка подключения>`<br>

Примеры строки подключения: 

* `qemu:///system` - локальный сервер
* `qemu+ssh://root@ip/system` - удаленный сервер по адресу **ip**

`virsh list [--inactive | --all]` - список виртуальных машин [отключенных | всех]<br>
`virsh start <domain>` - запуск вирт. машины **domain**<br>
`virsh shutdown <domain>` - остановка вирт. машины **domain**<br>
`virsh destroy <domain>` - разрушить (остановить) вирт. машину<br>
`virsh reboot <domain>` - перезагрузить вирт. машину<br>
`virsh reset <domain>` - перезагрузить вирт. машину(эмуляция нажатия кнопки *reset*)<br>
`virsh define <domain>` - определить (но не запускать) домен из файла XML<br>
`virsh undefine <domain>` - удаление вирт. машины из определенных доменов(убрать из списка)<br>
`virsh suspend <domain>` - приостановить вирт. машину<br>
`virsh resume <domain>` - продолжить работу вирт. машины<br>
`virsh save <domain> <file>` - сохранить состояние вирт. машины в файл<br>
`virsh restore <file>` - восстановить состояние вирт. машины из файла<br>
`virsh edit <domain>` - редактирование XML-конфигурации вирт. машины<br>


# virt-viewer
Подключение к vnc<br>
`virt-viewer -c <строка подключение> <domain>`


# virt-install
Установка вирт. машин<br>
Имеет много опций, которые можно посмотреть по комманде `man virt-install`<br>


# virt-manager
Графическая утилита для работы с libvirt
