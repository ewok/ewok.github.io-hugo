---
date: 2016-02-22T17:50:45+03:00
description: HuGo and Go
keywords:
- go
tags:
- go
title: HuGo and Go
type: post
---

![](/images/2016/02/gopher_head.png)

Во первых, я очередной раз сменил блоговый движок. На этот раз я остановил свой выбор на [hugo](http://gohugo.io). Hugo - генератор статичных страниц, написанный на [Go](https://golang.org/). Довольно таки зрелый продукт. Подробнее познакомиться с ним можно на [официальной странице](http://gohugo.io).

Во вторых, я познакомился с языком [Go](https://golang.org). Я нашел что язык мне симпатичен, прост в освоении и удобен в повседневных задачах devops инженера, и не только.

Основными плюсами для меня стали:

-	Хорошая поддержка кроссплатформенности
-	Скорость выполнения
-	Параллелизм
-	Компиляция в один бинарник, без зависимостей

Очень удобно написать какую нибудь небольшую программку, закинуть ее на сервер и не думать о сторонних библиотеках(как например в python).

Есть конечно и минусы, но язык относительно молодой и будем надеяться с каждым релизом будет еще лучше.

Материалы по Go для начала:
---------------------------

-	Первое на что наткнулся, это [Краткий пересказ Effective Go на русском языке](http://eao197.narod.ru/desc/short_effective_go.html) - вещь довольно старая но еще актуальная.
-	Непосредственно сам [Effective Go](https://golang.org/doc/effective_go.html)
-	[Go в примерах](https://gobyexample.com/)
-	[Build web application with Golang](https://www.gitbook.com/book/astaxie/build-web-application-with-golang/details)

Тулзовины:
----------

-	Продвинутый парсинг аргументов - [go-flags](https://github.com/jessevdk/go-flags)
-	Для работы с github - [go-github](https://github.com/google/go-github)
-	Конвертер curl запросов в код Go - [curl-to-go](http://mholt.github.io/curl-to-go/)
-	Работаем с elasticsearch - [elastigo](https://github.com/mattbaird/elastigo)
-	Для любителей VIM - [vim-go](https://github.com/fatih/vim-go)
-	Работа с yaml - [go-yaml](https://github.com/go-yaml/yaml)
-	Демонизируем программу - [daemonigo](https://github.com/tyranron/daemonigo) -
-	Посылаем метрику в ганглию - [go-gmetric](https://github.com/jbuchbinder/go-gmetric)
-	Рефлексируем структуры - [structs](https://github.com/fatih/structs)
-	Делаем дашборд в терминале - [termui](https://github.com/gizak/termui)
-	VPN с помощью DHT - [meshbird](https://github.com/meshbird/meshbird)
