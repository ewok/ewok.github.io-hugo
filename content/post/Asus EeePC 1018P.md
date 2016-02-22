{
    "date": "2011-01-29",
    "description": null,
    "draft": false,
    "id": 5,
    "image": null,
    "meta_title": null,
    "slug": "asus-eeepc-1018p",
    "tags": [
        "offline"
    ],
    "title": "Asus EeePC 1018P",
    "type": "post"
}



Железо: Нетбук Asus 1018P Экран - 10.1" (1024x600)

Процессор - Atom DualCore N550 (1.5GHz)

Оперативная память - 1GB DDR3

Жесткий диск - 250GB

Плюс: Bluetooth 3.0, Wi-Fi, WebCam 0.3 MPx, CardReader (SD, MMC), USB 3.0, LAN, 4 cell battery, Windows 7 Starter RU Вес - 1.1 кг

Ядро Установил Ubuntu 10.10. Ядро 2.6.35.

По умолчанию встало всё кроме: wifi и suspend/hibernate, сканера отпечатков пальцев.

Решил собрать ядро 2.6.37. По ссылке находятся файлы для сборки ядра плюс драйвера для wifi карточки. Файл "config" уже почти готовая настройка для сборки ядра под eeepc 1018p, требующая небольшой доработки.

make menuconfig

Во первых нужно указать количество процессоров - 4:

Processor type and features ---> Maximum number of CPUs

Во вторых указать поддержку USB 3.0:

Device Drivers ---> USB support ---> xHCI HCD (USB 3.0) support

Всё

	make
	make modules_install install reboot`

Установка драйверов на wifi:

Распаковываем hybrid-portscr_xxx_xx-v_xxx_xx_xx.tar.gz в /usr/src/bcmwl-xxx.xx.xx

Патчи копируем в папку bcmwl-xxx.xx.xx/patches

Далее при условии что у вас установлен dkms(если нет то лучше поставить :) )

Создаем файл в этой же папке под названием dkms.conf c таким содержанием:

	PACKAGE_NAME="bcmwl"
	PACKAGE_VERSION="XXX.XX.XX"
	CLEAN="rm -f *.*o"
	BUILT_MODULE_NAME[0]="wl"
	MAKE[0]="make -C $kernel_source_dir
	M=$dkms_tree/$PACKAGE_NAME/$PACKAGE_VERSION/build"
	DEST_MODULE_LOCATION[0]="/updates"

	# Указываем патчи

	# PATCH[0]="license.patch"
	# PATCH[1]="mutex-sema.patch"
	# PATCH[2]="semaphore.patch"
	# Needed for 2.6.35 and later AUTOINSTALL="yes"

Далее выполняем:

	sudo dkms add -m bcmwl -v xxx.xx.xx
	sudo dkms build -m bcmwl -v xxx.xx.xx
	sudo dkms install -m bcmwl -v xxx.xx.xx`

Вместо xx - указываем версию

После этого нерабочим остался режим hibernate и сканер отпечатков пальцев.

Ищу решение.
