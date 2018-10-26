---
title: "Подводные камни при использовании Fabric(SSH) и Jenkins"
date: 2013-09-16T23:15:00+03:00
draft: False
category: [Linux,Web Development]
tags: [fabrik,ssh,jenkins]
archives: [2013]
aliases:
    - post/problems-with-using-fabric-ssh-and-jenkins.aspx
---


Или мне так не везет, или для всех это совершенно очевидные вещи, но я, при выполнении простой fabric task'и копирования содержимого директорий, столкнулся на ряд проблем, которые хоть и казались простыми и распростаренными, но были описаны в найденных мной блогах и мануалах в плной мере.

## Проблема #1 - неправильный пользователь

Не всегда бывает что имя локального пользователя совпадает с удаленным. Ситуация распространенная и описанная всеми, кому не лень. Решение простое - указывем нужного пользователя в переменной env.user:

**from fabric.api import *<br />env.user = 'e0ne'**

## Проблема #2 - аутентификация

Самый простой способ аутентификации по SSH - имя пользователя и пароль. Самая распространенная проблема - нужно как-то безопасно хранить пароль. А так, как я предпочитаю все скрипты для развертывания хранить в VCS (читать как в git’е), то возникает проблема: нехорошо хранить пароль в репозитории, особенно в открытом на GitHub’е. Решение простое - использование пары public/private RSA ключей. Процесс генерации и настройки (ключевые слова: **ssh-keygen**, **~/.ssh/known_hosts**) описывать сейчас не буду, только то, что касается Jenkins’а.

В моем случае, Jenkins был установлен на Ubuntu server 13.04 командой  “**apt-get install jenkins**”, поэтому пользователь jenkins в системе создался таким образом, что без подоплнительной настройки под ним не залогинишься. Поэтому использем sudo и генерируем ключи для подключения по SSH, примерно, так:

**$ sudo -u jenkins -i ssh-keyget -t rsa**

После чего в домашнем каталоге jenkins’а будет лежать пара ключей, публичный из которых нужно положить на наш сервер, на который fabric будет копировать файлы. Достатьid_rsa.pub можно так:

**$ sudo -u jenkins -i cat ~/.ssh/id_rsa.pub**

И положить этот ключ на сервер, в моем случае в файл **/home/e0ne/.ssh/known_hosts.**

Этот способ так же решает проблему того, что не нужно передавать в fabric путь к ключу, он будет браться из пути по умолчанию.

## Проблема # 3 - не загружаются файлы

Ошибка тут у меня была совсем непонятной (привет paramiko и протоколу ssh), откатывать настройки или делать это с другим сервером сейчас нет возможности. Да и точно не помню как я пришел к решению. Наверное, после медитации на вывод команды “ls -al”. Задача jenkins job’ы была в том, что нужно было апдейтить простое веб-приложение, а у пользователя, под которым jenkins/fabric подключался к серверу не было прав на запись в нужную директорию. Решилось добавлением пользователя в группу www-data, в которой у меня находится пользователь nginx’а.

Пока все. Эти три проблемы были при попытке “простого копирования” файлов. Дальше будет должно быть интереснее. Или проще. Как повезет:).
