{
    "date": "2010-12-01",
    "description": null,
    "draft": false,
    "id": 3,
    "image": null,
    "meta_title": null,
    "slug": "stumpwm",
    "tags": [
        "admins"
    ],
    "title": "Stumpwm",
    "type": "post"
}




Stumpwm - легкий, тайловый оконный менеджер, написанный полностью на Common Lisp. Stumpwm является переделкой автора, менеджера окон ratpoison, написанного на C. Установку я производил двух видов. В первом варианте(по умолчанию) собирал исполняемый файл, во втором запускал из исходников с подключением slime, для ковыряния в менеджере так сказать в "прямом эфире".


**Установка:**

**Вариант 1.**

Подразумевается что у вас уже установлен какой либо лисп пакет. Я покажу на примере sbcl. Запускаем консоль и выполняем:

`$ sbcl * (require 'asdf) * (require 'asdf-install) * (asdf-install:install 'clx) * (asdf-install:install 'cl-ppcre)`

Этим самым мы устанавливаем два пакета clx и cl-ppcre, необходимые для работы stumpwm.

Затем непосредственно сама сборка и установка:

`$ autoconf $ ./configure $ make`

Если всё прошло успешно мы получим исполняемый файл stumpwm. Копируем его куда-нибудь для дальнейшего запуска и прописываем к нему пусть в ~/.xinitrc.


`$ echo exec /path_to_stumpwm/stumpwm >> ~/.xinitrc`

Всё перезапускаем иксы и наслаждаемся.


**Вариант 2.**

Имеем установленный sbcl, slime, clx и cl-ppcre.

Включаем stumpwm.asd в пакет sbcl, то есть прописываем символическую ссылку в каталог где sbcl ищет пакеты. Например:

`ln -s /path_to_stumpwm/stumpwm.asd ~/.sbcl/systems`

Создаем файл startstump, который будет запускать slime и stumpwm, примерно такого содержания:

`(require :stumpwm) (require :swank) (swank-loader::setup) (swank:create-server :dont-close t) (stumpwm:stumpwm) (quit)`

Прописываем в ~/.xinitrc запуск это файла:

`$ echo exec sbcl --load /path_to_startstump/startstump >> ~/.xinitrc`

Перезапускаем иксы.

Запускаем emacs и подключаемся к REPL stumpwm.

В emacs: M-x slime

Всё, теперь у нас есть доступ напрямую изменять stumpwm.
