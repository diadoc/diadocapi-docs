Структуры данных
================

Для сериализации/десериализации структур данных, передаваемых в HTTP запросах и ответах, составляющих интеграторский интерфейс Диадока, можно использовать следующие механизмы:

-  `Google Protocol Buffers <https://developers.google.com/protocol-buffers/>`__,

-  `JSON <http://json.org/json-ru.html>`__

По умолчанию все структуры ожидаются в формате Protocol Buffers, так как он считается основным форматом для передачи данных. 

Мы рекомендуем для интеграционных решений использовать формат Protocol Buffers, так как у него есть ряд преимуществ по сравнению с форматом JSON - одно из основных это обратная совместимость.

В JSON поддерживаются только последние версии структур данных.

Прежде чем выбирать формат передачи данных, рекомендуем ознакомиться с данной статьей - http://blog.codeclimate.com/blog/2014/06/05/choose-protocol-buffers/


Google Protocol Buffers
-----------------------

Описание синтаксиса языка Protocol Buffers можно посмотреть `здесь <https://developers.google.com/protocol-buffers/docs/proto>`__.

Для различных платформ и языков программирования существуют уже готовые библиотеки, рещающие задачу сериализации/десериализации родных структур данных в протобуферы. Вот некоторые из них:

-  C++, Java, Python - `официальная реализация Google <https://github.com/google/protobuf>`__;

-  Microsoft® .NET - `проект protobuf-net <https://code.google.com/p/protobuf-net/>`__;

-  и другие - `много ссылок <https://github.com/google/protobuf/wiki/Third-Party-Add-ons>`__.

Актуальная версия инструментария для разработчиков https://diadoc.kontur.ru/sdk/ также содержит все необходимые для использования интеграторского интерфейса Диадока библииотеки.

При помощи суффикса ``?proto``, добавляемого к имени любой команды, можно получить актуальное описание всех структур данных (см. :doc:`Структуры данных <DataStructures>`), необходимых для использования этой команды.

Например, по запросу https://diadoc-api.kontur.ru/GetBox?proto выдается описание структуры данных :doc:`Box <proto/Organization>`.

JSON
----

Для передачи структур в формате JSON, нужно передать следующий заголовки запроса:

- Заголовок ``Accept: application/json`` - указывается для получения структур в формате JSON в теле ответа, 

- Заголовок ``Content-Type: application/json charset=utf-8`` - указывается для передачи структур в формате JSON в теле запроса,
  
По умолчанию, состав всех структур в обоих форматах одинаков, если не сказано обратного.

Бинарный контент следует передавать с помощью :rfc:`base64<4648#section-4>` - строк.

Пример описания
---------------

Например, если  :doc:`proto/SearchDocflowsRequest` можно описать следующим образом.

В формате Protocol Buffers:


.. code-block:: protobuf

   message SearchDocflowsRequest
   {
       required string QueryString = 1;
       optional int32 Count = 2 [default = 100];
       optional int32 FirstIndex = 3;
       optional SearchScope Scope = 4 [default = SearchScopeAny];
       optional bool InjectEntityContent = 5 [default = false];
   }

   enum SearchScope
   {
       SearchScopeAny = 0;
       SearchScopeIncoming = 1;
       SearchScopeOutgoing = 2;
       SearchScopeDeleted = 3;
       SearchScopeInternal = 4;
   }

В формате JSON:

.. code-block:: json

   {  
       "QueryString": "example",
       "Count": 100,
       "FirstIndex": 1,
       "Scope": 0,
       "InjectEntityContent": false
   }