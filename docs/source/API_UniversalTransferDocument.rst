Работа с УПД
============

Для упрощения работы с API существует `SDK (C#) <https://github.com/diadoc/diadocsdk-csharp/releases>`__, скрывающий детали взаимодействия по HTTP и позволяющий работать с API через набор функций.

Генерация УПД
-------------

.. toctree::
   :name: utdGeneration
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/GenerateTitleXml
   http/GenerateReceiptXml

Отправка УПД
------------

.. toctree::
   :name: utdSign
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/utd/ExtendedSignerDetailsV2
   http/PrepareDocumentsToSign
   http/PostMessage
   http/PostMessagePatch

Парсинг УПД
------------

.. toctree::
   :name: utdParsing
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/ParseTitleXml

Структуры данных
----------------

.. toctree::
   :name: toc4
   :maxdepth: 1
   :titlesonly:
   :glob:

   proto/utd/*
   proto/PrepareDocumentsToSignRequest
   proto/PrepareDocumentsToSignResponse
