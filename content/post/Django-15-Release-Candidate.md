---
title: "Django 1.5 Release Candidate"
date: 2013-01-09T23:50:00+03:00
draft: False
category: [Python,Web Development]
tags: [django]
archives: [2013]
aliases:
    - post/Django-15-Release-Candidate.aspx
---


4 января вышел релиз кандидат fullstack-фрейморка для разработки веб-приложения Django. Обзоры, наверено, не писали/читали только ленивые. Но пишут, в основном, про мажорные фичи, из-за которых и выпускают релиз. Я перевел свой небольшой прототипчик одного приложения на Django 1.5 RC и поюзал некоторые минорные нововведения, о которых пишут мало, но которые почти делают каждый релиз тем, из-за чего часто хочется использовать именно его. Из того, что мне понравилось - это:


<ul>
- изменения в template engine: теперь True, False, None воспринимаются так же, как и в python;
- дополнительные батарейки для работы с временными зонами - мелочь, а очень приятно;
- исправленна ошибка OutOfMemory при использовании команды dumpdata - особенно полезно на небольших хостингах;
- mod_wsgi auth handler - для тех, кто все еще использует Apache и Basic авторизацию;
- в debug конфигурации приложения логи дополнительно выводятся в консоль;
- user_login_failed событие - понятно что это такое, +1 к секьюрити: легче блокировать ботов от перебора паролей и плюс к защите от DDoS;
- loaddata имеет опцию для игнорирования колонок, которых больше нет в модели - просто в восторге от этой фичи, имхо, она для меня теперь станет неаменимой при разработке, кода модель активно меняется, а django south использовать еще рано (в момент разработки, а не при выходе в production).
</ul>
Из всего вышесказанного, кроме mod_wsgi auth handler попробовал все и хоче сказать: дявол кроется в деталях, они делают любой продукт именно таким, чтоб им (не) хотелось пользоваться.
<br />
Ну и не могу сказать про одно мажорное изменения - эксперементальная поддержка Python 3.2+! Осталось подождать и/или портировать нужные зависимости для проектов и можно начинать использовать. На свой страх и риск, конечно, т.к. production код должен быть как можно стабильнее, а не в статусе "эксперементальная фича". Хотя, time to market никто не отменял...
<br />
Подробности на оффициальном сайте Django:

<ul>
- [https://www.djangoproject.com/weblog/2013/jan/04/15-rc-1/](https://www.djangoproject.com/weblog/2013/jan/04/15-rc-1/)
- [https://docs.djangoproject.com/en/dev/releases/1.5/](https://docs.djangoproject.com/en/dev/releases/1.5/)
</ul>



- [https://www.djangoproject.com/weblog/2013/jan/04/15-rc-1/](https://www.djangoproject.com/weblog/2013/jan/04/15-rc-1/)
- [https://docs.djangoproject.com/en/dev/releases/1.5/](https://docs.djangoproject.com/en/dev/releases/1.5/)
