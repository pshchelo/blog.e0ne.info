---
title: "tipfy - маленький, но мощьный web framework для GAE"
date: 2011-01-17T13:45:00+03:00
draft: False
category: [Python,Web Development]
tags: [python,gae]
archives: [2011]
aliases:
    - post/tipfy-small-but-powerful-framework-for-GAE.aspx
---


 

Так уж сложилось, что мне было необходимо выбрать framework для разработки небольшого приложения на python + GAE. Первым делом я посмотрел в сторону Django и немного огорчился, узнав что теперь GAE team рекомендуют использовать форк [django-nonrel](http://www.allbuttonspressed.com/projects/django-nonrel) - практически тот же django, но дающий возможность простой работы с NoSQL базами данных. Так как django-nonrel все ещё не достиг версии 1.0 и имеет ряд недоработок, которые разработчики обещают исправить в ближайшее время. Из недостатков, которые для меня оказались решающими стоит отметить - не работает с GAE “из коробки”, соответственно необходимо многое доустанавливать-настраивать руками, на что не хотелось тратить время. Позже я обязательно напишу про этот фреймворк, но уже на примере django-nonrel + MongoDB. Тем временем мне порекомендовали посмотреть в сторону tipfy, на котором я остановился и о котором написан этот пост.

Как написано на сайте [http://www.tipfy.org/](http://www.tipfy.org/), tipfy - маленький, но мощьный web framework, сделанный специально для GAE (“tipfy is a small but powerful framework made specifically for Google App Engine”). Текущая версия - 0.6.4, что говорит нам о том, что у него всё ещё впереди.

tipfy действительно очень маленький и быстрый, но благодаря расширениям (extensions) быстро приобретает необходимую функциональность. Посмотрим на структуру архива, который можно скачать по адресу [http://www.tipfy.org/tipfy.zip](http://www.tipfy.org/tipfy.zip)

 

 

<img src="/image.axd?picture=2011%2f1%2fdirectories.png" alt="" />

 

Всё, что лежит в корне архиве необходимо только для сборки своей версии tipfy, с добавленными или отключенными расширениями. К слову, добавление или отключение какого-либо расширение осуществляется редактированием всего одной строчки в файле buildout.cfg и запуском билд-скрипта, который загрузит и установит нужные расширения. Подробнее об этом можно почитать на странице http://www.tipfy.org/wiki/guide/extensions/#adding-or-removing-extensions

 

Всё, что необходимо для запуска и работы приложения находится в каталоге app. Как видно на скриншоте, там уже есть приложение “hello world” (куда же без него? :)). После “hello world” сразу же бросается в глаза [jinja2](http://jinja.pocoo.org/) - достаточно известный template engine с хорошей докоментацией и сообществом. Если по каким-то причинам вам не нравится(перечеркнуто) подходит jinja, можно использовать [Genshi](http://www.tipfy.org/wiki/genshi/) или [Mako](http://www.tipfy.org/wiki/mako/).

В целом, приложение с использованием tipfy практически ничем не отличается от любого MVC-приложения, за исключением, конечно, специфики фреймворка.

Рассмотрим приложение “hello world” более детально.

Так как, это достаточно простой пример, то никакой модели нет. Но в случае необходимости - модели будут представлять собой обычные классы, наследуемые от GAE db.Model:

<img src="/image.axd?picture=2011%2f1%2fmodel.png" alt="" />

 

Наше приложение состоит из двух модулей (url.py и handlers.py) и одного шаблона (hello_world.html).

****urls.py:****

Содержит правила маппинга url-адресов на обработчики. По умолчанию их два:

 

- **Rule('/', endpoint='hello-world', handler='apps.hello_world.handlers.HelloWorldHandler')** - указывает какой обработчик должен обрабатывать default page
- **Rule('/pretty', endpoint='hello-world-pretty', handler='apps.hello_world.handlers.PrettyHelloWorldHandler')** - обработчик, который выполнится при открытии [http://yoursite.com/pretty](http://yoursite.com/pretty)

 

****handlers.py:****

Каджый handler представляет собой класс, который наследуется от RequestHandler и имеет методы get(), post и др. для обработки соответствующих типов запросов.

В нашем случай это: 

 

 

<img src="/image.axd?picture=2011%2f1%2fhandlers.png" alt="" />

 

В целом отмечу что переход с django на tipfy не вызывает никаких трудностей, только несколько маленьких неудобств, а именно: отсутствие уже готовой админки (частично, её может заменить аналога приложения в GAE) и другой template engine (хотя, многие успешно используют jinja в djanпo).

Такое короткое введение в tipfy и GAE. Продолжение следует...

 

