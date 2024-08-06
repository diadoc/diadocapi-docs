OutboundUniversalTransferDocumentDocflow
========================================

.. warning::
	Структура устарела.

Структура ``OutboundUniversalTransferDocumentDocflow`` представляет собой информацию о документообороте исходящего УПД.

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

- ``IsFinished`` — признак того, что документооборот завершен и документ не требует дальнейших действий.
- ``ReceiptDocflow`` — информация об извещении о получении, отправленном в ответ на полученный УПД, представленная структурой :doc:`InboundInvoiceReceiptDocflow`.
- ``ConfirmationDocflow`` — информация о подтверждении даты доставки УПД, представленная структурой :doc:`InvoiceConfirmationDocflow`. Формируется оператором.
- ``CorrectionRequestDocflow`` — информация о запросе уточнения УПД, представленная структурой :doc:`InvoiceCorrectionRequestDocflow`.
- ``ConfirmationTimestamp`` — время подтверждения даты доставки, представленное структурой :doc:`../Timestamp`.
- ``IsAmendmentRequested`` — признак того, что по УПД было запрошено уточнение.
- ``IsRevised`` — признак того, что УПД был исправлен (на него сформировано исправление).
- ``IsCorrected`` — признак того, что УПД был откорректирован (на него сформирована корректировка).
- ``CanDocumentBeSignedBySender`` — признак того, что документ может быть подписан отправителем. Принимает значение ``true`` для входящих документов, сохраненных для последующей отправки, либо для исходящих документов с некорректной подписью.
- ``BuyerTitleDocflow`` — информация об ответной подписи под документом, представленная структурой :doc:`BuyerTitleDocflow`. Ответная подпись для формализованных двусторонних документов представляет собой подписанный файл установленного формата: например, титул покупателя для товарной накладной, или титул заказчика для акта.
- ``RecipientSignatureRejectionDocflow`` — информация об отказе в подписании документа получателем, представленная структурой :doc:`RecipientSignatureRejectionDocflow`. Заполняется только в случае если отказ был.
- ``IsReceiptRequested`` — признак того, что по документу было запрошено извещение о получении.
- ``IsRecipientSignatureRequested`` — признак того, что по документу запрошена ответная подпись.
- ``IsDocumentSignedByRecipient`` — признак того, что документ подписан получателем.
- ``IsDocumentRejectedByRecipient`` — признак того, что получатель отказал в подписи документа.
- ``CanDocumentBeReceipted`` — признак того, что для документа можно отправить извещение о получении. Принимает значение ``true`` для входящих документов, по которым корректные извещения ранее не отправлялись.
- ``CanDocumentBeSignedOrRejectedByRecipient`` — признак того, что получатель может подписать документ или отказать в подписании.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`Docflow`