UniversalCorrectionDocumentInfo
===============================

.. code-block:: protobuf

    message UniversalCorrectionDocumentInfo
    {
        optional string TotalInc = 1;
        optional string TotalDec = 2;
        optional string VatInc = 3;
        optional string VatDec = 4;
        optional int32 CurrencyCode = 5;
        optional string Grounds = 6;
        required FunctionType Function = 7;
        optional DocumentDateAndNumber OriginalDocumentDateAndNumber = 8;
        optional DocumentDateAndNumber OriginalDocumentRevisionDateAndNumber = 9;
        optional DocumentDateAndNumber OriginalDocumentCorrectionDateAndNumber = 10;
    }

Структура представляет метаданные документов, имеющих :doc:`тип <../../DocumentType>` *UniversalCorrectionDocument* или *UniversalCorrectionDocumentRevision*.

-  *TotalInc* - сумма с учетом налога, всего к увеличению.

-  *TotalDec* - сумма с учетом налога, всего к уменьшению.

-  *VatInc* - сумма налога, всего к увеличению.

-  *VatDec* - сумма налога, всего к уменьшению.

-  *CurrencyCode* - код валюты.

-  *Grounds* - описание оснований для данного документа.

-  *Function* - функция документа, описывается структурой :doc:`FunctionType <../UniversalTransferDocumentSellerTitleInfo>`.

-  :doc:`OriginalInvoiceDateAndNumber <../../DocumentDateAndNumber>` - дата и номер исходного УПД (заполняется, если корректировка была сформирована на УПД).

-  :doc:`OriginalInvoiceRevisionDateAndNumber <../../DocumentDateAndNumber>` - дата и номер исходного исправления УПД (заполняется, если корректировка была сформирована на исправление УПД).

-  :doc:`OriginalInvoiceCorrectionDateAndNumber <../../DocumentDateAndNumber>` - дата и номер исходной УКД (заполняется, если корректировка была сформирована на УКД).
