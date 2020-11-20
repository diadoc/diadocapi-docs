Работа со счетами-фактурами
===========================

Для упрощения работы с API существует SDK (C#/C++/Java/COM), скрывающий детали взаимодействия по HTTP и позволяющий работать с API через набор функций.

Генерация СФ
-------------

.. toctree::
   :name: invoiceGeneration
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/CanSendInvoice
   http/GenerateTitleXml
   http/GenerateReceiptXml
   http/GetInvoiceCorrectionRequestInfo

Отправка СФ
-----------

.. toctree::
   :name: invoiceSign
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/utd/ExtendedSignerDetailsV2
   http/PrepareDocumentsToSign
   http/PostMessage
   http/PostMessagePatch

Парсинг СФ
----------

.. toctree::
   :name: invoiceParsing
   :maxdepth: 1
   :titlesonly:
   :glob:

   http/ParseTitleXml

Структуры данных
----------------

.. toctree::
   :name: invoceStruct
   :maxdepth: 1
   :titlesonly:
   :glob:

   proto/utd/*
   proto/PrepareDocumentsToSignRequest
   proto/PrepareDocumentsToSignResponse
