InboundInvoiceDocflow
=====================

.. code-block:: protobuf

   message InboundInvoiceDocflow
   {
       optional bool IsFinished = 1;
       optional InboundInvoiceReceiptDocflow ReceiptDocflow = 2;
       optional InvoiceConfirmationDocflow ConfirmationDocflow = 3;
       optional InvoiceCorrectionRequestDocflow CorrectionRequestDocflow = 4;
       optional Timestamp ConfirmationTimestamp = 5;
       optional bool IsAmendmentRequested = 6;
       optional bool IsRevised = 7;
       optional bool IsCorrected = 8;
   }

Структура представляет информацию о документообороте входящего счёта-фактуры.

-  *IsFinished* - признак завершенности документооборота.
-  :doc:`ReceiptDocflow <InboundInvoiceReceiptDocflow>` - информация об извещении о получении, отправленном в ответ на полученный счёт-фактуру.
-  :doc:`ConfirmationDocflow <InvoiceConfirmationDocflow>` - информация о подтверждении даты доставки счёта-фактуры (формируется оператором).
-  :doc:`CorrectionRequestDocflow <InvoiceCorrectionRequestDocflow>` - информация о запросе уточнения счёта-фактуры.
-  :doc:`ConfirmationTimestamp <Timestamp>` - метка времени подтверждения даты доставки.
-  *IsAmendmentRequested* - признак того, что по счёту-фактуре было запрошено уточнение.
-  *IsRevised* - признак того, что счёт-фактура был исправлен (на него сформировано исправление).
-  *IsCorrected* - признак того, что счёт-фактура был откорректирован (на него сформирована корректировка).
