Работа с УПД
============

Для упрощения работы с API существует SDK (C#), скрывающий детали взаимодействия по HTTP и позволяющий работать с API через набор функций.

Генерация УПД
-------------

.. toctree::
   :name: utdGeneration
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/utd/GenerateUniversalTransferDocumentXmlForSeller
   http/utd/GenerateUniversalTransferDocumentXmlForBuyer
   http/GenerateInvoiceDocumentReceiptXml

Отправка УПД
------------

.. toctree::
   :name: utdSign
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/utd/ExtendedSignerDetails
   http/PostMessage
   http/PostMessagePatch

Парсинг УПД
------------

.. toctree::
   :name: utdParsing
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/utd/ParseUniversalTransferDocumentSellerTitleXml
   http/utd/ParseUniversalTransferDocumentBuyerTitleXml

Структуры данных
----------------

.. toctree::
   :name: toc4
   :maxdepth: 1
   :titlesonly:
   :glob:

   proto/utd/*
