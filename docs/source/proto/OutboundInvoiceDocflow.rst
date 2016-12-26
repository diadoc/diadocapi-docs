OutboundInvoiceDocflow
======================

.. code-block:: protobuf

   message OutboundInvoiceDocflow
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
   }

Структура представляет информацию о документообороте исходящего счёта-фактуры.

-  *IsFinished* - признак завершенности документооборота.

-  :doc:`ReceiptDocflow` - информация об извещении о получении, отправленном в ответ на счёт-фактуру.

-  :doc:`ConfirmationDocflow <InvoiceConfirmationDocflow>` - информация о подтверждении даты отправки (формируется оператором).

-  :doc:`CorrectionRequestDocflow <InvoiceCorrectionRequestDocflow>` - информация о запросе уточнения.

-  :doc:`ConfirmationTimestamp <Timestamp>` - метка времени подтверждения даты отправки.

-  *IsAmendmentRequested* - признак того, что по счёту-фактуре было запрошено уточнение.

-  *IsRevised* - признак того, что счёт-фактура был исправлен (на него сформировано исправление).

-  *IsCorrected* - признак того, что счёт-фактура был откорректирован (на него сформирована корректировка).

-  *CanDocumentBeSignedBySender* - признак того, что счёт-фактура может быть подписан отправителем. Значение true может означать, что документ был сохранен без подписи и готов к отправке, или уже был подписан, но подпись была признана некорректной.
