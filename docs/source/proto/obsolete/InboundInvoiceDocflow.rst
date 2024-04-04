InboundInvoiceDocflow
=====================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``InboundInvoiceDocflow`` представляет собой информацию о документообороте входящего счета-фактуры.

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

- ``IsFinished`` — признак того, что документооборот завершен и документ не требует дальнейших действий.
- ``ReceiptDocflow`` — информация об извещении о получении, отправленном в ответ на полученный счет-фактуру, представленная структурой :doc:`InboundInvoiceReceiptDocflow`.
- ``ConfirmationDocflow`` — информация о подтверждении даты доставки счета-фактуры, представленная структурой :doc:`InvoiceConfirmationDocflow`. Формируется оператором.
- ``CorrectionRequestDocflow`` — информация о запросе уточнения счета-фактуры, представленная структурой :doc:`InvoiceCorrectionRequestDocflow`.
- ``ConfirmationTimestamp`` — время подтверждения даты доставки, представленное структурой :doc:`../Timestamp`.
- ``IsAmendmentRequested`` — признак того, что по счету-фактуре было запрошено уточнение.
- ``IsRevised`` — признак того, что счет-фактура был исправлен (на него сформировано исправление).
- ``IsCorrected`` — признак того, что счет-фактура был откорректирован (на него сформирована корректировка).

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Docflow`.

*Руководства:*
	- :doc:`../../Docflow API`