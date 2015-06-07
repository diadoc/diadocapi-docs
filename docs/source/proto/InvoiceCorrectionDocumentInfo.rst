InvoiceCorrectionDocumentInfo
=============================

.. code-block:: protobuf

   message InvoiceCorrectionDocumentInfo
   {
       optional string TotalInc = 1;
       optional string TotalDec = 2;
       optional string VatInc = 3;
       optional string VatDec = 4;
       optional int32 CurrencyCode = 5;
       optional DocumentDateAndNumber OriginalInvoiceDateAndNumber = 6;
       optional DocumentDateAndNumber OriginalInvoiceRevisionDateAndNumber = 7;
       optional DocumentDateAndNumber OriginalInvoiceCorrectionDateAndNumber = 8;
   }

Структура представляет метаданные документов, имеющих :doc:`тип <DocumentType>` InvoiceCorrection или InvoiceCorrectionRevision.

-  *TotalInc* - сумма с учетом налога, всего к увеличению.
-  *TotalDec* - сумма с учетом налога, всего к уменьшению.
-  *VatInc* - сумма налога, всего к увеличению.
-  *VatDec* - сумма налога, всего к уменьшению.
-  *CurrencyCode* - код валюты.
-  :doc:`OriginalInvoiceDateAndNumber <DocumentDateAndNumber>` - дата и номер исходного счёта-фактуры (заполняется, если корректировка была сформирована на счёт-фактуру).
-  :doc:`OriginalInvoiceRevisionDateAndNumber <DocumentDateAndNumber>` - дата и номер исходного исправления счёта-фактуры (заполняется, если корректировка была сформирована на исправление счёта-фактуры).
-  :doc:`OriginalInvoiceCorrectionDateAndNumber <DocumentDateAndNumber>` - дата и номер исходной корректировки счёта-фактуры (заполняется, если корректировка была сформирована на корректировку счёта-фактуры).
