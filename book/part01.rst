Введение
============

Symfony2 является связкой переиспользуемых, слабосвязанных компонентов,
решаюших большинство задач веб-разработки на PHP.

Вместо того, чтобы использовать эти низкоуровневые компоненты, вы можете взять
готовый Symfony2, полноценный фреймворк, основанный на этих компонентах. Или же
создать ваш собственный фреймворк. Серия этих статей как раз о втором варианте

.. note::

    Если вы просто хотите использовать полноценный Symfony2, вам лучше обратиться
    к оффициальной документации `documentation`_.

Почему вам хочется создать свой фреймворк?
------------------------------------------------

Why would you like to create your own framework in the first place? If you
look around, everybody will tell you that it's a bad thing to reinvent the
wheel and that you'd better choose an existing framework and forget about
creating your own altogether. Most of the time, they are right but I can think
of a few good reasons to start creating your own framework:

* To learn more about the low level architecture of modern web frameworks in
  general and about the Symfony2 full-stack framework internals in particular;

* To create a framework tailored to your very specific needs (just be sure
  first that your needs are really specific);

* To experiment creating a framework for fun (in a learn-and-throw-away
  approach);

* To refactor an old/existing application that needs a good dose of recent web
  development best practices;

* To prove the world that you can actually create a framework on your own (...
  but with little effort).

I will gently guide you through the creation of a web framework, one step at a
time. At each step, you will have a fully-working framework that you can use
as is or as a start for your very own. We will start with simple frameworks
and more features will be added with time. Eventually, you will have a
fully-featured full-stack web framework.

And of course, each step will be the occasion to learn more about some of the
Symfony2 Components.

.. tip::

    If you don't have time to read the whole series, or if you want to get
    started fast, you can also have a look at `Silex`_, a micro-framework
    based on the Symfony2 Components. The code is rather slim and it leverages
    many aspects of the Symfony2 Components.

Many modern web frameworks call themselves MVC frameworks. We won't talk about
MVC here as the Symfony2 Components are able to create any type of frameworks,
not just the ones that follow the MVC architecture. Anyway, if you have a look
at the MVC semantics, this series is about how to create the Controller part
of a framework. For the Model and the View, it really depends on your personal
taste and I will let you use any existing third-party libraries (Doctrine,
Propel, or plain-old PDO for the Model; PHP or Twig for the View).

When creating a framework, following the MVC pattern is not the right goal.
The main goal should be the Separation of Concerns; I actually think that this
is the only design pattern that you should really care about. The fundamental
principles of the Symfony2 Components are focused on the HTTP specification.
As such, the frameworks that we are going to create should be more accurately
labelled as HTTP frameworks or Request/Response frameworks.

Before we start
---------------

Reading about how to create a framework is not enough. You will have to follow
along and actually type all the examples we will work on. For that, you need a
recent version of PHP (5.3.8 or later is good enough), a web server (like
Apache or NGinx), a good knowledge of PHP and an understanding of Object
Oriented programming.

Ready to go? Let's start.

Bootstrapping
-------------

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
.. _`autoload`:                  http://fr.php.net/autoload
.. _`Composer`:                  http://packagist.org/about-composer
.. _`PSR-0`:                     https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
.. _`Symfony2 Coding Standards`: http://symfony.com/doc/current/contributing/code/standards.html
.. _`ClassLoader`:               http://symfony.com/doc/current/components/class_loader.html
