OutboundUniversalTransferDocumentDocflow
========================================

.. code-block:: protobuf

    message OutboundUniversalTransferDocumentDocflow
    {
        optional bool IsFinished = 1;
        optional ReceiptDocflow ReceiptDocflow = 2;
        optional InvoiceConfirmationDocflow ConfirmationDocflow = 3;
        optional InvoiceCorrectionRequestDocflow CorrectionRequestDocflow = 4;
        optional Timestamp ConfirmationTimestamp = 5;
        optional bool IsAmendmentRequested = 6;
        optional bool IsRevised = 7;
        optional bool IsCorrected = 8;
        optional bool CanDocumentBeSignedBySender = 9;
        optional BuyerTitleDocflow BuyerTitleDocflow = 10;
        optional RecipientSignatureRejectionDocflow RecipientSignatureRejectionDocflow = 11;
        optional bool IsReceiptRequested = 12;
        optional bool IsRecipientSignatureRequested = 13;
        optional bool IsDocumentSignedByRecipient = 14;
        optional bool IsDocumentRejectedByRecipient = 15;
        optional bool CanDocumentBeReceipted = 16;
        optional bool CanDocumentBeSignedOrRejectedByRecipient = 17;
    }

Структура представляет информацию о документообороте входящего УПД.

-  *IsFinished* - признак завершенности документооборота.

-  :doc:`ReceiptDocflow <../../InboundInvoiceReceiptDocflow>` - информация об извещении о получении, отправленном в ответ на полученный УПД.

-  :doc:`ConfirmationDocflow <../../InvoiceConfirmationDocflow>` - информация о подтверждении даты доставки УПД (формируется оператором).

-  :doc:`CorrectionRequestDocflow <../../InvoiceCorrectionRequestDocflow>` - информация о запросе уточнения УПД.

-  :doc:`ConfirmationTimestamp <../../Timestamp>` - метка времени подтверждения даты доставки.

-  *IsAmendmentRequested* - признак того, что по УПД было запрошено уточнение.

-  *IsRevised* - признак того, что УПД был исправлен (на него сформировано исправление).

-  *IsCorrected* - признак того, что УПД был откорректирован (на него сформирована корректировка).

-  *CanDocumentBeSignedBySender* - признак того, что документ может быть подписан отправителем. Равен ``true`` для документов, сохраненных для последующей отправки, либо для исходящих документов с некорректной подписью.

-  :doc:`../../BuyerTitleDocflow` - информация об ответной подписи под документом. Ответная подпись для формализованных двусторонних документов представляет собой подписанный файл установленного формата (например, титул покупателя для товарной накладной, или титул заказчика для акта).

-  :doc:`../../RecipientSignatureRejectionDocflow` - информация об отказе в подписании документа получателем. Заполняется только в том случае, когда отказ был.

-  *IsReceiptRequested* - признак того, что по документу было запрошено извещение о получении.

-  *IsRecipientSignatureRequested* - признак того, что по документу запрошена ответная подпись.

-  *IsDocumentSignedByRecipient* - признак того, что документ подписан получателем.

-  *IsDocumentRejectedByRecipient* - признак того, что получатель отказал в подписи документа.

-  *CanDocumentBeReceipted* - признак того, что для документа можно отправить извещение о получении. Равен true для входящих документов, по которым корректные извещения ранее не отправлялись.

-  *CanDocumentBeSignedOrRejectedByRecipient* - признак того, что получатель может подписать документ или отказать в подписании.
