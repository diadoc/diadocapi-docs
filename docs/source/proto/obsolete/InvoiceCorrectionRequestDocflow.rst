InvoiceCorrectionRequestDocflow
===============================

.. warning::
	Структура устарела.

Структура ``InvoiceCorrectionRequestDocflow`` представляет собой информацию об уведомлении об уточнении (УоУ) счета-фактуры.

.. code-block:: protobuf

   message InvoiceCorrectionRequestDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment CorrectionRequestAttachment = 2;
       optional ReceiptDocflow ReceiptDocflow = 3;
   }

- ``IsFinished`` — признак того, что документооборот УоУ завершен: уведомление имеет корректную подпись и на него было получено извещение о получении с корректной подписью.
- ``CorrectionRequestAttachment`` — информация о файле УоУ, представленная структурой :doc:`../SignedAttachment`.
- ``ReceiptDocflow`` — информация об извещении о получении данного запроса, представленная структурой :doc:`ReceiptDocflow`.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`InboundInvoiceDocflow`
	- в устаревшей структуре :doc:`InboundUniversalTransferDocumentDocflow`
	- в устаревшей структуре :doc:`OutboundInvoiceDocflow`
	- в устаревшей структуре :doc:`OutboundUniversalTransferDocumentDocflow`