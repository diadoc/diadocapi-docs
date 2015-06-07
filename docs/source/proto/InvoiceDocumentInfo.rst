InvoiceDocumentInfo
===================

.. code-block:: protobuf

   message InvoiceDocumentInfo
   {
       optional string Total = 1;
       optional string Vat = 2;
       optional int32 CurrencyCode = 3;
       optional DocumentDateAndNumber OriginalInvoiceDateAndNumber = 4;
   }

Структура представляет метаданные документов, имеющих :doc:`тип <DocumentType>` Invoice или InvoiceRevision.

-  *Total* - сумма с учетом НДС, всего по документу.
-  *Vat* - сумма НДС, всего по документу.
-  *CurrencyCode* - код валюты.
-  :doc:`OriginalInvoiceDateAndNumber <DocumentDateAndNumber>` - только для InvoiceRevision: дата и номер исходного счёта-фактуры.
