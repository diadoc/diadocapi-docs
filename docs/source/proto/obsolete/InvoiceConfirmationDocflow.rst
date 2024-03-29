InvoiceConfirmationDocflow
==========================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``InvoiceConfirmationDocflow`` представляет собой информацию о подтверждении оператора в рамках документооборота счета-фактуры.

.. code-block:: protobuf

   message InvoiceConfirmationDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment ConfirmationAttachment = 2;
       optional ReceiptDocflow ReceiptDocflow = 3;
   }

- ``IsFinished`` — признак того, что документооборот подтверждения завершен. Принимает значение ``true`` в случае если подтверждение имеет корректную подпись и оператором в ответ на это подтверждение было получено извещение о получении с корректной подписью.
- ``ConfirmationAttachment`` — информация о файле подтверждения, представленная структурой :doc:`../SignedAttachment`.
- ``ReceiptDocflow`` — информация об извещении о получении данного подтверждения, представленная структурой :doc:`ReceiptDocflow`.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`InboundInvoiceDocflow`,
	- в структуре :doc:`InboundInvoiceReceiptDocflow`,
	- в структуре :doc:`InboundUniversalTransferDocumentDocflow`,
	- в структуре :doc:`OutboundInvoiceDocflow`,
	- в структуре :doc:`OutboundUniversalTransferDocumentDocflow`.

*Руководства:*
	- :doc:`../../Docflow API`