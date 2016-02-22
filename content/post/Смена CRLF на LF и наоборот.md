{
    "date": "2013-10-19",
    "description": null,
    "draft": false,
    "id": 34,
    "image": null,
    "meta_title": null,
    "slug": "smiena-crlf-na-lf-i-naoborot",
    "tags": [
        "admins"
    ],
    "title": "Смена CRLF на LF и наоборот",
    "type": "post"
}


CRLF -> LF

	# вариант с sed. Что-бы получить символ '^M' нужно использовать 'Ctrl+V Ctrl+M'
	$ sed 's/^M$//' input.txt > output.txt

	# или
	$ tr -d '\r' < input.file > output.file

LF -> CRLF

	$ sed 's/$'"/`echo \\\r`/" input.txt > output.txt

в nix можно установить утилиту dos2unix
