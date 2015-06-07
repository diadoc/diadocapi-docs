Работа со счетами-фактурами
===========================

Для упрощения работы с API существует SDK (C#/C++/Java/COM), скрывающий детали взаимодействия по HTTP и позволяющий работать с API через набор функций.

HTTP-интерфейс
--------------

.. toctree::
   :name: toc3
   :maxdepth: 1
   :titlesonly:

   http/CanSendInvoice
   http/GenerateInvoiceXml
   http/GenerateInvoiceCorrectionRequestXml
   http/GenerateInvoiceDocumentReceiptXml
   http/GetInvoiceCorrectionRequestInfo
   http/ParseInvoiceXml

Структуры данных
----------------

.. toctree::
   :name: toc4
   :maxdepth: 1
   :titlesonly:

   proto/InvoiceCorrectionInfo
   proto/InvoiceCorrectionRequestInfo
   proto/InvoiceDocumentMetadata
   proto/InvoiceInfo