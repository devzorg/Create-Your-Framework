Введение
========

Symfony2 является связкой переиспользуемых, слабосвязанных компонентов,
решаюших большинство задач веб-разработки на PHP.

Вместо того, чтобы использовать эти низкоуровневые компоненты, вы можете взять
готовый Symfony2, полноценный фреймворк, основанный на этих компонентах. Или же
создать ваш собственный фреймворк. Серия этих статей как раз о втором варианте

    Если вы просто хотите использовать полноценный Symfony2, вам лучше обратиться
    к оффициальной документации `documentation`_.

Почему вам хочется создать свой фреймворк?
------------------------------------------

Для начала разберемся в причинах, из-за чего вам хочется создать свой
фреймворк, что вами движет? Если оглянуться вокруг, каждый скажет, что
изобретать велосипед - плохо. Возьмите что-то готовое, а о создании своего
и думать забудьте. Скорее всего они будут правы, но я могу предложить
несколько аргументов в поддержку идеи создания собственного фреймворка:

* Узнать больше о низкоуровневой архитектуре современных веб-фреймворков в
  общем и Symfony2 в частности;

* Создать узкоспециализированную структуру приложения (только сначала убедитесь,
  действительно ли на столько спецефична эта структура будет);

* Экспереминт, просто для развлечения (с подходом: научись и выброси);

* Рефакторинг старого приложения, нуждающегося в использовании последних лучших
  практик веб разработки;

* Доказать миру, что вы способны разработать свой фреймворк.

Я осторожно проведу вас по всем этапам создания веб фреймворка, поэтапно.
На каждом этапе у вас будет полностью рабочий фреймворк, который можно будет
использовать как есть, или создать на его основе что-то свое. Мы начнем с простого
и будем постепенно улучшать, добавляя новую функциональность. В конце концов у вас
получится полноценный веб-фреймворк.

И конечно на каждый шаг позволит узнать больше о компонентах Symfony2.

    Если у вас нет времени на чтение всей серии статей, или вы хотите побыстрее
    начать, вы можете также изучить `Silex`_, микро-фреймворк, основанный на
    компонентах Symfony. В Silex довольно немного кода, но в в полной мере
    реализована философия Symfony2.

Большинство современных фреймворков объявляют себя MVC-фреймворками. Мы не
будем обсуждать здесь MVC, потому как компоненты Symfony2 могут быть использованы
для создания фреймворка любой архитектуры. Так или иначе, если рассматривать эту
часть с точки зрения MVC, мы будем говорит о C - части фреймворка отвечающей, за
организацию контроллеров. Модель и Представление зависит от ваших персональных
предпочтений и я предлагаю вам использовать любые сторонние библиотеки для этого
(Doctrine, Propel, или устаревший чистый PDO для Модели; PHP или `Twig`_ для Представления).

Когда создаешь фреймворк, следование паттерну MVC не правильная цель. Основной целью
должно стать разделение обязанностей; На самом деле я думаю это единственный архитектурный
паттерн, о котором вам следует постоянно думать. Компоненты Symfony2 сфокусированны на
спецификации HTTP. Таким образом следует отметить, что мы собираемся создавать
так называемый HTTP фреймворк, или Запрос - Ответ - фреймворк.

Прежде чем начать
-----------------

Просто прочитать о создании фреймворка не достаточно. Вам прийдется проверять
весь код, который мы напишем. Для этого вам требуется последняя версия PHP (5.3.8
или выше будет достаточно), сервер (например Apache, или Nginx) хорошее понимание PHP и
Объектно-ориентированного программирования.

Готовы? Начнем!

Загрузчик
---------

Before we can even think of creating our first framework, we need to talk
about some conventions: where we will store our code, how we will name our
classes, how we will reference external dependencies, etc.

To store our framework, create a directory somewhere on your machine:

.. code-block:: sh

    $ mkdir framework
    $ cd framework

Components Installation
~~~~~~~~~~~~~~~~~~~~~~~

To install the Symfony2 Components that we need for our framework, we are
going to use `Composer`_, a project dependency manager for PHP. Create a
``composer.json`` file, where we will list our dependencies:

.. code-block:: javascript

    {
        "require": {
        }
    }

The file is empty for now as we do not depend on anything yet. To install the
project dependencies, download the composer binary and run it:

.. code-block:: sh

    $ wget http://getcomposer.org/composer.phar
    $ # or
    $ curl -O http://getcomposer.org/composer.phar

    $ php composer.phar install

After running the ``install`` command, you must see a new ``vendor/``
directory.

Naming Conventions and Autoloading
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We are going to `autoload`_ all our classes. Without autoloading, you need to
require the file where a class is defined before being able to use it. But
with some conventions, we can just let PHP do the hard work for us.

Symfony2 follows the de-facto PHP standard, `PSR-0`_, for class names and
autoloading and Composer generates such an autoloader for all the dependencies
it manages; it can be enabled by requiring the ``vendor/autoload.php`` file.

Our Project
-----------

Instead of creating our framework from scratch, we are going to write the same
"application" over and over again, adding one abstraction at a time. Let's
start with the simplest web application we can think of in PHP::

    <?php

    // framework/index.php

    $input = $_GET['name'];

    printf('Hello %s', $input);

That's all for the first part of this series. Next time, we will introduce the
HttpFoundation Component and see what it brings us.

.. _`documentation`:             http://symfony.com/doc
.. _`Silex`:                     http://silex.sensiolabs.org/
.. _`Twig`:                      http://twig.sensiolabs.org/
.. _`autoload`:                  http://fr.php.net/autoload
.. _`Composer`:                  http://packagist.org/about-composer
.. _`PSR-0`:                     https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
.. _`Symfony2 Coding Standards`: http://symfony.com/doc/current/contributing/code/standards.html
.. _`ClassLoader`:               http://symfony.com/doc/current/components/class_loader.html
