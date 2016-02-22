{
    "date": "2012-02-22",
    "description": null,
    "draft": false,
    "id": 84,
    "image": null,
    "meta_title": null,
    "slug": "hibernate-chieriez-pm-utils",
    "tags": [
        "dev"
    ],
    "title": "hibernate через pm-utils",
    "type": "post"
}


В русской вики arch в статье о pm-utils там где описывается настройка hibernate, почему то не указано что нужно прописывать hook: resume для в mkinitcpio.

Поэтому у меня в hibernate уходил комп нормально, но не возвращался из него. Рекомендую читать английский вариант статьи там все прописано.

В итоге все выглядит так:

В файл /boot/grub/menu.lst добавляется resume=/path/to/swap/drive

    # (0) Arch Linux 
    title Arch Linux root (hd0,0) 
    kernel /vmlinuz26 root=/dev/sda3 resume=/dev/sda2 ro vga=0 
    initrd /kernel26.img

Или вариант с UUD:

    # (0) Arch Linux 
    title Arch Linux root (hd0,0) 
    kernel /vmlinuz26 cryptdevice=/dev/sda2:main root=/dev/mapper/main-root \
     resume=/dev/disk/by-uuid/1d893194-b151-43cd-a89e-6f89bd8b9f99 ro 

    initrd /kernel26.img

В файле /etc/mkinitcpio.conf добавляется хук resume после scsi pata но перед filesystems:

    HOOKS="base udev fsck autodetect pata scsi sata usb resume filesystems usbinput shutdown"
 
 У меня все заработало. Для более тонких настроек читайте вики.
