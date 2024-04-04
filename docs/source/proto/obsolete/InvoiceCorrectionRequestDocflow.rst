InvoiceCorrectionRequestDocflow
===============================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

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
	- в структуре :doc:`InboundInvoiceDocflow`,
	- в структуре :doc:`InboundUniversalTransferDocumentDocflow`,
	- в структуре :doc:`OutboundInvoiceDocflow`,
	- в структуре :doc:`OutboundUniversalTransferDocumentDocflow`.

*Руководства:*
	- :doc:`../../Docflow API`