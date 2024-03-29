OutboundInvoiceDocflow
======================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``OutboundInvoiceDocflow`` представляет собой информацию о документообороте исходящего счета-фактуры.

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

- ``IsFinished`` — признак того, что документооборот завершен и документ не требует дальнейших действий.
- ``ReceiptDocflow`` — информация об извещении о получении, отправленном в ответ на счет-фактуру, представленная структурой :doc:`ReceiptDocflow`.
- ``ConfirmationDocflow`` — информация о подтверждении даты отправки, представленная структурой :doc:`InvoiceConfirmationDocflow`. Формируется оператором.
- ``CorrectionRequestDocflow`` — информация о запросе уточнения, представленная структурой :doc:`InvoiceCorrectionRequestDocflow`.
- ``ConfirmationTimestamp`` — время подтверждения даты отправки, представленное структурой :doc:`../Timestamp`.
- ``IsAmendmentRequested`` — признак того, что по счету-фактуре было запрошено уточнение.
- ``IsRevised`` — признак того, что счет-фактура был исправлен (на него сформировано исправление).
- ``IsCorrected`` — признак того, что счет-фактура был откорректирован (на него сформирована корректировка).
- ``CanDocumentBeSignedBySender`` — признак того, что счет-фактура может быть подписан отправителем. Принимает значение ``true`` в случаях:

   - если документ был сохранен без подписи и готов к отправке
   - если документ уже был подписан, но подпись была признана некорректной.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`Docflow`.

*Руководства:*
	- :doc:`../../Docflow API`