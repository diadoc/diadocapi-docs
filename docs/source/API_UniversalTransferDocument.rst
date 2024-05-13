Работа с УПД
============

Для упрощения работы с API существует `SDK (C#) <https://github.com/diadoc/diadocsdk-csharp/releases>`__, скрывающий детали взаимодействия по HTTP и позволяющий работать с API через набор функций.

Генерация УПД
-------------

.. toctree::
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/GenerateTitleXml
   http/GenerateReceiptXml

Отправка УПД
------------

.. toctree::
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/ExtendedSignerDetailsV2
   http/PrepareDocumentsToSign
   http/PostMessage
   http/PostMessagePatch

Парсинг УПД
------------

.. toctree::
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/ParseTitleXml

Структуры данных
----------------

.. toctree::
   :maxdepth: 1
   :titlesonly:
   :glob:

   proto/PrepareDocumentsToSignRequest
   proto/PrepareDocumentsToSignResponse
