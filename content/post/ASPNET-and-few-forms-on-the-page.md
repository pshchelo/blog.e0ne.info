---
title: "ASP.NET и несколько форм на одной странице"
date: 2011-05-05T14:41:00+03:00
draft: False
category: [.NET Framework,Web Development]
tags: [asp.net,html,forms]
archives: [2011]
aliases:
    - post/ASPNET-and-few-forms-on-the-page.aspx
---


 

Рассказ о “странном” баге и о том, как влияет верстка работу всего приложения.

При работе с ASP.NET Webforms мы постоянно сталкиваемся с формами. По умолчанию, это одна серверная форма **<form id=”aspnetForm” runat=”sever”>**, расположенная сразу же за тегом **<body>**. Но это, можно сказать, классический пример - такую заготовку делает нам Visual Studio при создании другого проекта. На практике же всё может сильно отличаться.

 

Следует отметить, что на странице вы не можете создать более одной серверной формы (с атрибутом** runat=”server”**). Такое уж ограничение архитектуры ASP.NET. Почему так - догадаться не сложно, но...

 

Но в жизни в проекте бывают ситуации, когда просто необходимо добавить ещё одну форму на страницу. Из достаточно распространённых примеров это: 

 

когда в шапке сайта где-то рядом с меню нужно разместить форму поиска, при этом, для увеличения скорости загрузки, сама шапка сайта находится вне серверной формы. Такой случай достаточно распространённый и уже практически стал стандартом де-факто для разработчиков.

 

Решение данной задачи достаточно простое - добавление второй формы (**<form>**) на страницу, но уже без атрибута **runat=”server”**. Следует отметить, что с точки зрения html - несколько форм на одной странице являются абсолютно нормальным и работающем решением. Если только не наступать та те же грабли, на которые наступил я...

 

А допустил я достаточно “детскую” ошибку - т.к. было ограничение на одну серверную форму, то я добавил вторую, клиентскую, внутрь серверной. На первый взгляд всё работало хорошо, обе формы успешно отправлялись на сервер и отправляли все необходимые данные. Вот только работало это в браузерах Google Chrome, Safari и FireFox. Проблемы начались в Opera и Internet Explorer. Выглядело это, на мой взгляд, действительно потрясающе: 

 

Форма фидбека с UpdatePanel двумя TextBox и LinkButton на странице. Обработчик OnClick у кнопки успешно отрабатывал, за исключением того, что значения текстбоксов были пустыми. Дело было вечером и я подумал что проблема в UpdatePanel. Вот только странно было что в IE это тоже не работало. Под нож попала UpdatePanel, что не дало никакого положительного результата. “Странно” - подумал я и проверил это всё ещё раз в разных браузерах. Баг был на месте. Тут пришлось вплотную взяться дебаггером за эту страницу и через некоторое время, внимательно посмотрев на Request.Params причина была обнаружена - сабмитилась не та форма.

 

Дальнейшие** танцы с бубном** возникшие идеи результата не принесли я на помощь пришел Google:

<img src="/image.axd?picture=2011%2f5%2fgoogle.png" alt="" />

 

 

Обрадовало меня сразу две вещи:

 

- такая проблема была не только у меня;
- причина всего этого безобразия стала ясна уже только при беглом просмотре результатов выдачи гугла - 3-я ссылка вела на сайт W3C, на которой черным по белому было написано: **“the FORM element can’t be nested”**. ([http://www.w3.org/MarkUp/html3/forms.html](http://www.w3.org/MarkUp/html3/forms.html))

 

 

После этого проблема была быстро решена способом, описанным в начале поста, но мне захотелось ещё немного копнуть внутрь.

 

Тут же был создан небольшой html файл (forms1.html)  и был дан валидатору http://validator.w3.org/. К моему удивлению, валидатор был уверен в том, что html код является полностью валидным. После смены doctype с Transitional на Strict (forms2.html) страница уже оказывалась невалидной. И тут всё окончательно прояснилось и стало на свои места.

 

С точки зрения html, как и с точки зрения здравого смысла - ничего хорошего не принесут. Всё дело лишь в том, что с годами некоторые браузеры стали настолько умными, что уже понимают практически все общеизвестные ошибки в вёрстке и делают это так, как, по их мнению, задумывалось. Отсюда и различное поведение одних страниц в разных браузерах, и попытки обойти проблемы одного браузера, не поломав ничего в других и т.д.

 

В который раз убеждаюсь в необходимости грамотного верстальщика на любом проекте и необходимости соблюдать html-стандарты на своих сайтах. Только не фанатично, у всех правил есть исключения...

 

Исходники форм: [https://github.com/e0ne/BlogSamples/tree/master/NestedForms](https://github.com/e0ne/BlogSamples/tree/master/NestedForms)

 

