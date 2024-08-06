InvoiceConfirmationDocflow
==========================

.. warning::
	Структура устарела.

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

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`InboundInvoiceDocflow`
	- в устаревшей структуре :doc:`InboundInvoiceReceiptDocflow`
	- в устаревшей структуре :doc:`InboundUniversalTransferDocumentDocflow`
	- в устаревшей структуре :doc:`OutboundInvoiceDocflow`
	- в устаревшей структуре :doc:`OutboundUniversalTransferDocumentDocflow`