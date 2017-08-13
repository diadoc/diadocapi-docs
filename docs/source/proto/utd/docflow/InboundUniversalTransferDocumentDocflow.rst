InboundUniversalTransferDocumentDocflow
=======================================

.. code-block:: protobuf

    message InboundUniversalTransferDocumentDocflow
    {
        optional bool IsFinished = 1;
        optional InboundInvoiceReceiptDocflow ReceiptDocflow = 2;
        optional InvoiceConfirmationDocflow ConfirmationDocflow = 3;
        optional InvoiceCorrectionRequestDocflow CorrectionRequestDocflow = 4;
        optional Timestamp ConfirmationTimestamp = 5;
        optional bool IsAmendmentRequested = 6;
        optional bool IsRevised = 7;
        optional bool IsCorrected = 8;
        optional BuyerTitleDocflow BuyerTitleDocflow = 9;
        optional RecipientSignatureRejectionDocflow RecipientSignatureRejectionDocflow = 10;
        optional bool IsReceiptRequested = 11;
        optional bool IsRecipientSignatureRequested = 12;
        optional bool IsDocumentSignedByRecipient = 13;
        optional bool IsDocumentRejectedByRecipient = 14;
        optional bool CanDocumentBeReceipted = 15;
        optional bool CanDocumentBeSignedOrRejectedByRecipient = 16;
    }

Структура представляет информацию о документообороте входящего УПД.

-  *IsFinished* - признак завершенности документооборота.

-  :doc:`ReceiptDocflow <../../InboundInvoiceReceiptDocflow>` - информация об извещении о получении, отправленном в ответ на полученный УПД.

-  :doc:`ConfirmationDocflow <../../InvoiceConfirmationDocflow>` - информация о подтверждении даты доставки УПД (СЧФ) (формируется оператором).

-  :doc:`CorrectionRequestDocflow <../../InvoiceCorrectionRequestDocflow>` - информация о запросе уточнения УПД (СЧФ).

-  :doc:`ConfirmationTimestamp <../../Timestamp>` - метка времени подтверждения даты доставки.

-  *IsAmendmentRequested* - признак того, что по УПД (СЧФ) было запрошено уточнение.

-  *IsRevised* - признак того, что УПД (СЧФ) был исправлен (на него сформировано исправление).

-  *IsCorrected* - признак того, что УПД (СЧФ) был откорректирован (на него сформирована корректировка).

-  :doc:`../../BuyerTitleDocflow` - информация об ответной подписи под документом. Ответная подпись для формализованных двусторонних документов представляет собой подписанный файл установленного формата (например, титул покупателя для товарной накладной, или титул заказчика для акта).

-  :doc:`../../RecipientSignatureRejectionDocflow` - информация об отказе в подписании документа получателем. Заполняется только в том случае, когда отказ был.

-  *IsReceiptRequested* - признак того, что по документу было запрошено извещение о получении.

-  *IsRecipientSignatureRequested* - признак того, что по документу запрошена ответная подпись.

-  *IsDocumentSignedByRecipient* - признак того, что документ подписан получателем.

-  *IsDocumentRejectedByRecipient* - признак того, что получатель отказал в подписи документа.

-  *CanDocumentBeReceipted* - признак того, что для документа можно отправить извещение о получении. Равен true для входящих документов, по которым корректные извещения ранее не отправлялись.

-  *CanDocumentBeSignedOrRejectedByRecipient* - признак того, что получатель может подписать документ или отказать в подписании.
