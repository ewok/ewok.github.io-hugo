{
    "date": "2014-05-05",
    "description": null,
    "draft": false,
    "id": 14,
    "image": null,
    "meta_title": null,
    "slug": "bibliotieka-sh-dlia-python",
    "tags": [
        "dev"
    ],
    "title": "Библиотека sh для python",
    "type": "post"
}


Классная штука. Позволяет обращаться к командам shell в контексте языка python. Примеры из документации:

	from sh import ifconfig
	print(ifconfig("wlan0"))

	# checkout master branch
	git.checkout("master")

	# print(the contents of this directory
	print(ls("-l"))

	# get the longest line of this file
	longest_line = wc(\_\_file\_\_, "-L")

	from sh import git, sudo

	# resolves to "git branch -v"
	print(git.branch("-v"))
	print(git("branch", "-v")) # the same command

	# resolves to "sudo /bin/ls /root"
	print(sudo.ls("/root"))
	print(sudo("/bin/ls", "/root")) # the same command

Единственное замечание это с вызовами имен файлов по маске. Вот это не сработает:

	import sh
	sh.ls("*.py")`

Нужно так:

	import sh
	sh.ls(sh.glob("*.py"))

Подробнее в документации
