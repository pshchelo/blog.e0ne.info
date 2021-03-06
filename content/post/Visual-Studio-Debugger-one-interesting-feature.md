---
title: "Visual Studio Debugger: одна интересная особенность"
date: 2010-07-21T15:10:00+03:00
draft: False
category: [.NET Framework]
tags: [visual studio,debugger]
archives: [2010]
aliases:
    - post/Visual-Studio-Debugger-one-interesting-feature.aspx
---


Когда приложение работает в дебаггере, но не работает в релизной сборке и/или не тестовом сервере - достаточно частое явление, а вот чтоб наоборот - значительно реже. Вернее я на днях с этим столкнулся чуть ли не в первые.

Ситуация была довольно таки простая: есть некий wizard, шаги которого хранятся в поле типа Stack для удобного перемещения вперёд-назад. Естественно, в зависимости от текущего номера шага, нужно было выполнять определённые действия. И вот, после очередного багфикса, пришлось с помощь дебаггера разбираться что же там происходит... Но, при дебагге время от времени (в начале мне было абсолютно непонятно из-за чего это происходит) я получал: ****System.InvalidOperationException: Stack empty****. И это при том, что без дебаггера всё работало! Чтоб разобраться в чем дело, я решил написать маленькое консольное приложение (исходники, как всегда, прикреплены к посту), которое состояло из объявления стека, его наполнения и свойства класса StackItem:

 <img src="/image.axd?picture=2010%2f7%2f1.jpg" alt="" />

<img src="/image.axd?picture=2010%2f7%2f2.jpg" alt="" />

Те, кто сталкивался с этим раньше, наверное, уже поняли в чем проблема. Запускаем дебаггер, и после наполнения стека смотрим значения свойства StackItem:

 

<img src="/image.axd?picture=2010%2f7%2f3.jpg" alt="" />

Второй раз смотрим значения свойства StackItem:

<img src="/image.axd?picture=2010%2f7%2f4.jpg" alt="" />

И здесь произошло самое интересное: при просмотре значения свойства дебаггер **выполняет** весь код, который находится в конструкции get. Таким образом, при каждом просмотре зачения свойства StackItem, в нашем стеке находилось все меньше и меньше данных. Возможно, для кого-то этот подход и является вполне логичным и очевидным, но не для меня. Ведь могли же в Microsoft предусмотреть это? Но нет, теперь у нас есть такая фича дебаггера, или баг...

А пока, для дебагга подобного кода, приходится использовать конструкцию вида:

 

<img src="/image.axd?picture=2010%2f7%2f5.jpg" alt="" />

В этом случае, если переменной i не присвоить другого значения, но она всегда будет хранить в себе число 5.

P.S. Проверял как в VS2008, так и в VS2010. Скорее всего, это фича такая...

[DebuggerTest.rar (2.74 kb)](/file.axd?file=2010%2f7%2fDebuggerTest.rar)

