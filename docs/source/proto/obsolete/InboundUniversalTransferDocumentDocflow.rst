InboundUniversalTransferDocumentDocflow
=======================================

.. warning::
	Структура используется внутри устаревшей структуры :doc:`Docflow`.

Структура ``InboundUniversalTransferDocumentDocflow`` представляет собой информацию о документообороте входящего УПД.

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

- ``IsFinished`` — признак того, что документооборот завершен и документ не требует дальнейших действий.
- ``ReceiptDocflow`` — информация об извещении о получении, отправленном в ответ на полученный УПД, представленная структурой :doc:`InboundInvoiceReceiptDocflow`.
- ``ConfirmationDocflow`` — информация о подтверждении даты доставки УПД (СЧФ), представленная структурой :doc:`InvoiceConfirmationDocflow`. Формируется оператором.
- ``CorrectionRequestDocflow`` — информация о запросе уточнения УПД (СЧФ), представленная структурой :doc:`InvoiceCorrectionRequestDocflow`.
- ``ConfirmationTimestamp`` — время подтверждения даты доставки, представленное структурой :doc:`../Timestamp`.
- ``IsAmendmentRequested`` — признак того, что по УПД (СЧФ) было запрошено уточнение.
- ``IsRevised`` — признак того, что УПД (СЧФ) был исправлен (на него сформировано исправление).
- ``IsCorrected`` — признак того, что УПД (СЧФ) был откорректирован (на него сформирована корректировка).
- ``BuyerTitleDocflow`` — информация об ответной подписи под документом, представленная структурой :doc:`BuyerTitleDocflow`. Ответная подпись для формализованных двусторонних документов представляет собой подписанный файл установленного формата: например, титул покупателя для товарной накладной или титул заказчика для актаS.
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
	- в структуре :doc:`Docflow`