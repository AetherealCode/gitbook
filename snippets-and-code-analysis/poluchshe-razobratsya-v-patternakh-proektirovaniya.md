# Получше разобраться в паттернах проектирования

[https://gist.github.com](https://gist.github.com/search?utf8=%E2%9C%93&q=%D0%BC%D0%B0%D0%BD%D0%B8%D1%84%D0%B5%D1%81%D1%82+google+play&ref=searchresults)/ база данных сниппетов и частей кодов  
[https://toster.ru/q/670238](https://toster.ru/q/670238) справочник по кодингу  
[https://docs.djangoproject.com/en/2.2/howto/custom-management-commands/](https://docs.djangoproject.com/en/2.2/howto/custom-management-commands/) кодинг на джанго  
[https://docs.celeryproject.org/en/latest/django/first-steps-with-django.html](https://docs.celeryproject.org/en/latest/django/first-steps-with-django.html) джанго  
[https://www.yiiframework.ru/forum/viewtopic.php?f=19&t=51084&p=248641\#p248641](https://www.yiiframework.ru/forum/viewtopic.php?f=19&t=51084&p=248641#p248641)  
  
Выжимка из ответов и комментариев:  


* Yii для обучения не очень\(больше подходит для быстрого кодинга\). Вместо рекомендуют Symfony
* Смотреть и анализировать чужой код\(думаю очевидно\)
* Елисеев Д. Неделя ООП Третий поток \(видеокурс\)
* "Чистый код" Роберт Мартин
* "Рефакторинг" Фаулер
* "PHP. Объекты, шаблоны и методики программирования" - сам читаю и сам тоже советую
* "Чистая архитектура" Роберт Мартин
* "Паттерны проектирования" 

целом, если вы хотите получше разобраться в паттернах проектирования - можно брать любую хорошую книжку по этой теме \(те же [Gang of Four](https://habr.com/ru/post/210288/), [Мартин Фаулер](https://www.martinfowler.com/eaaCatalog/) \([на русском](http://design-pattern.ru/patterns/)\) и т.п., предложенная [Ярослав](http://toster.ru/user/yaroslavche) ссылка тоже выглядит весьма достойно\), изучать, а затем пытаться найти эти паттерны в коде популярных и хорошо написанных проектов.  
  
Я несколько предвзят, но могу порекомендовать Symfony и Doctrine в качестве отправных точек. К примеру та же Doctrine прямо реализует целый пласт паттернов, описанных Фаулером. Symfony существенно более разнообразна, там можно встретить много различных решений.  
Если говорить о второй версии \(третья ещё не вышла\), то в Yii есть масса весьма сомнительных решений с точки зрения архитектуры:  
  
Это и ActiveRecord, который в целом многими считается антипаттерном из-за того что в одном объекте смешиваются и сами данные и бизнес-логика и логика взаимодействия с базой и т.п.  
  
Это и глобальное хранилище сервисов Yii::$app \(такой же есть и в Laravel, кстати\), откуда все подряд классы пытаются дёргать информацию вместо использования честного IoC \(inverse of control, часть принципов SOLID\).  
  
Это "толстые" контроллеры и "тонкие" модели \(последнее, в частности, является следствием использование ActiveRecord\).  
  
Это отсутствие шаблонизатора и использование PHP для рендера views что с одной стороны открывает существенное пространство для проблем с безопасностью, а с другой \(в том числе за счёт глобального Yii::$app\) - открывает недисциплинированным программистам возможности делать во views то что там делать нельзя \(никогда не видели запросов к базе из views?\)  
  
Ну и так далее...  
  
Я с ним мало работал, так что часть информации - из внешних источников, но в целом Yii - он про скорость разработки, а не про построение decoupled архитектуры.  
  
Yii может быть вполне неплохим выбором как фреймворк для относительно быстрой разработки, когда скорость получения результата важнее его качества. Для быстрого старта, построения MVP и не особо сложных / долгоживущих проектов он вполне может быть более подходящим чем, к примеру, тот же Symfony, но ведь в вопросе речь идёт именно об изучении хороших подходов к архитектуре, а здесь Yii - не лучший вариант.  
  
Развернуть и настроить проект на симфони - пара минут. Есть [CLI](https://symfony.com/download), есть [maker](https://symfony.com/doc/current/bundles/SymfonyMakerBundle/index.html#configuration) \(лично я лучшего генератора скаффолда не встречал в других фреймворках\). Есть всевозможные бандлы которые хендлятся плагином композера [flex](https://github.com/symfony/flex) \(пакинг/анпакинг пакетов и прочие ништяки\).  
  
К примеру, Вам нужно сайт с админкой и апи:  
composer create-project symfony/skeleton mySite && cd mySitecomposer require api admincomposer require --dev maker profiler symfony/web-serverbin/console server:start  
  
Потом сгенерируйте пару entity с помощью maker.  
А дальше уже посмотрите, что будет в итоге \(после небольшого курения мануала и конфигурации бандлов\). Уверен, Вы будете в восторге =\)  
Прошу заметить, что Вы будете иметь приложение НЕ НАПИСАВ НИ ОДНОЙ строчки на PHP =\)  
Написано [18 авг.](https://toster.ru/q/658688#comment_1977362)  
самом деле [Ярослав](http://toster.ru/user/yaroslavche) очень точно заметил что на Symfony зачастую нужно писать весьма мало кода для реализации **хорошего** решения.  
  
Особенно это заметно начиная с 4-й версии когда в дополнение к действительно грандизоному по своему удобству autowiring'у добавился Symfony Flex, почти полностью устранив необходимость в ручной конфигурации устанавливаемых пакетов.  
  
Если вы используете PHPStorm \(если нет - то крайне рекомендую\), то для него есть просто [шикарный плагин](https://plugins.jetbrains.com/plugin/7219-symfony-support/) для интеграции с Symfony, а также прекраснейшее дополнение к встроенным inspections - [PHP Inspections](https://plugins.jetbrains.com/plugin/7622-php-inspections-ea-extended-). Используя эту связку вы довольно скоро начинаете замечать что код пишется чуть ли не сам т.к. вам по большей части необходимо задумываться только о логике вашего приложения, всё остальное за вас делают инструменты.  
  
Поверьте после этого написание кода в других связках framework + soft можно расценивать как пытку... Приходится поддерживать проект на ZF2 и иметь дело с Wordpress, так что есть с чем сравнить :\)  
  
  
Гуглите "паттерны проектирования" и выбирайте что Вас интересует. Пример: [https://refactoring.guru/ru/design-patterns](https://refactoring.guru/ru/design-patterns)  

