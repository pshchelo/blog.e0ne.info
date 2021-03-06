---
title: "Стартапы. Взгляд со стороны разработчика"
date: 2011-07-01T14:47:00+03:00
draft: False
category: [Offtopic]
tags: []
archives: [2011]
aliases:
    - post/Startup-for-Developer-What-is-it.aspx
---


О стартапах пока не написал только ленивый. Говорят о них много, громко, красиво. Если раньше говорили только об успешных, то сейчас, кроме success stories все чаще слышно и об обратной стороны медали - провалах. Как маленьких, так и настоящих epic fail’ах.

Если верить википедии, то стартап - это:

Стартап или стартап-компания (от** англ. start-up — запускать) — компания с короткой историей операционной деятельности. Как правило, такие компании созданы недавно, находятся в стадии развития или исследования перспективных рынков. Термин стартап стал популярным во времена пузыря доткомов, когда было создано большое количество доткомов. Новые проекты в отраслях высоких технологий часто называют хайтек стартап. Также нужно отметить что хотя этот термин можно применять ко всем сферам деятельности, однако преимущественно он получил распространение в сфере IT и интернет проектов.<br />**[**http://ru.wikipedia.org/wiki/Стартап**](http://ru.wikipedia.org/wiki/Стартап)

Если коротко и без цензуры - быстро что-то сделали, продали/заработали кучу денег и радуемся жизни.

Слово “стартапер” в некоторых кругах стало модным, в некоторых ([Стартапер vs Предприниматель](http://dennydov.blogspot.com/2011/06/vs.html)) - ругательством. Но я хотел высказать свои мысли немного о другом. А именно:

Стартап с точки зрения разработчика: стоит ли работать в таком? делать свой?

Так как на объективность я не претендую, то можно писать то, что думаю.

### Часть 1. Работа в стартапе

Должно быть прикольно - выпустить на рынок новый продукт/услугу, получить фидбек от пользователей и при этом заработать кучу денег(зачеркнуто) получить свою зарплату. Мало чем отличается от аутсорса или продуктовой разработки. Основное отличие - вау-эффект, атмосфера в команде.

Ещё раз уточню: в данном случае, как правило, разработчик работает или за зарплату или за долю в проекте, т.е. за какуе-то будущую прибыль, размер которой заранее не известен, как и факт того, что эта самая прибыль всё-таки будет.

### Часть 2. Я сделаю свой стартап!

Это звучит громко, пафосно, красиво. Это может помочь заработать славу и много денег. Ну или потратить все свои деньги и, кроме отрицательного счета в банке, ничего не получить. Но ведь можно и заработать! Хотя мало кто думает над том, сколько % стартапов добиваются успехов. <br />“Но я же крутой разработчик, я смогу это сделать!” - скажут некоторые и начнут писать код для реализации чуть ли не первой попавшейся идеи. И тут начинается самое интересное...

Не важно, с какими мыслями разработчик дошел до этого момента, важно то, что будет раньше.

Тут я хочу сразу ответить на возможные вопросы на счёт моего маленьго проектика notacash.com, у котором я уже писал раньше. Я НЕ считаю это стартапом. Пока это просто небольшая сайтик, который помогает некоторым людям и делает их жизнь лучше и/или интереснее. Что будет с ним дальше - сложно сказать, поживём - увидем, но пусть пока работает, разговор о другом...

А сейчас я хочу рассказать о моменте, в котором разработчик решает сделать свой проект/продукт. В этот момент на голову разработчика сыпятся куча вопросов, о которых раньше не задумывался. Конечно, количество этих вопросов напрямую связано с квалификацией разработчика, тем, чем он занимался на работе и в какой компании работал(ет).

Ведь теперь перед разработчиком не стоит задача в выпуске той или иной фичи. Задача стоит так: нужно выпустить готовый продук.

И тут, как говорится, нужен на все руки мастер: и разработчик, и руководитель проекта, и дизайнер, и проектировщик интерфейсов, и, даже, маркетолог с заказчиком! Те, кто учился в ВУЗах на специальности, связанные с программированием, знают, что есть стандартный жизненный цикл любого ПО. Так вот что я могу сказать по этому поводу. Жизненный цикл ПО - намного больше и обширнее, чем, по крайней мере, мне, рассказывали на соответствующих лекциях на парах. Всё сложнее и больше. Но это тема для совсем другого поста.

Вернемся к выпуску своего продукта и к проблемам, которыесваливаются на голову разработчика задачи и с которыми, вполне вероятно, раньше не приходилось заниматься. Написание ТЗ, планирование времени, создание простого и понятного пользовательского интерфейса и так далее.

Да, можно работать без четких эстимейтов и сроков, но рано или поздно в голову подкрадывается мысль: надо же показать это кому-то! И тут начинается предрелизная стадия. Это может быть выпуск beta- или alfa-версии, запуск рабочего прототипа или ещё что-то. Но, если в этот момент появляется желание выпустить этот продукт в мир, то забываются такие вещи, как:

- “Я буду использовать только самые новые технологии”
- “Что-то архитектура проекта не очень удачная, сейчас я всё быстренько переделаю...”
- “Перед релизом нужно сделать рефакторинг этого, этого и ещё того”
- и т.д.

После всего этого в работу подключается маркетолог. А тут вспоминается что далеко не каждый разработчик находился всегда в хороших отношениях с маркетологами и может стать таковым. И начинаются попытки как-то сделать так, чтоб на этот сайт заходило какое-то количество людей, большее 0. А тут ещё нужно фиксить баги, делать классные фичи, рефакторить и т.д.

Вообщем всё на много сложнее, чем кажется. Зато полученные опыт и знания обязательно будут полезны любому девелоперу. Т.ч. нужно очень хорошо подумать, прежде чем делать свой стартап и строить о нем какие-либо планы...

