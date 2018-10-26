---
title: "ASP.NET и правильный выбор имен классов"
date: 2008-06-27T14:21:00+03:00
draft: False
category: [Web Development]
tags: [asp.net]
archives: [2008]
aliases:
    - post/ASPNET-and-correct-class-names.aspx
---



На днях в очередной раз столкнулся с проблемой:  после разворачивания приложения на сервере на нескольких страницах появляется 500-я ошибка. Процесс развертывания приложения проходит следующим образом:


	- разработка и отладка приложения на машине разработчика
	- cборка проекта с помощью aspnet_compiler
	- коирование на тестовый сервер


На этих шагах все работает отлично, а дальше получаем стандартную желтую страницу с ошибкой о невозможности найти нужный класс. В данном случае проблема была со страницей восстановления пароля, на которой находился только компонент PasswordRecovery. Т.к. проект был собрал в release-версии, отадка была сильно затруднена.  Далее выяснилось, что класс, реализующий эту страницу тоже назывался PasswordRecovery. Таким образом, компиляция происходит успешно, но на этапе выполнения происходит исключение. Проблема состоит в том, что в одной области видимости появляется два класса с одним именем, и .net не знает какой класс нужно использовать.



Для решения проблемы следует либо обращатся к классам с указанием namespace (System.Web.UI.WebControls.PasswordRecovery), либо переименовать ваш класс (UserPasswordRecovery).  

