UniversalTransferDocumentInfo
=============================

.. code-block:: protobuf

    message UniversalTransferDocumentInfo
    {
        optional string Total = 1;
        optional string Vat = 2;
        optional int32 CurrencyCode = 3;
        optional string Grounds = 4;
        required FunctionType Function = 5;
        optional DocumentDateAndNumber OriginalDocumentDateAndNumber = 6;
    }

Структура представляет метаданные документов, имеющих :doc:`тип <../../DocumentType>` *UniversalTransferDocument* или *UniversalTransferDocumentRevision*.

-  *Total* - сумма с учетом НДС, всего по документу.

-  *Vat* - сумма НДС, всего по документу.

-  *CurrencyCode* - код валюты.

-  *Grounds* - описание оснований для данного документа.

-  *Function* - функция документа, описывается структурой :doc:`FunctionType <../UniversalTransferDocumentSellerTitleInfo>`.

-  :doc:`OriginalInvoiceDateAndNumber <../../DocumentDateAndNumber>` - только для *UniversalTransferDocumentRevision*: дата и номер исходного УПД.
