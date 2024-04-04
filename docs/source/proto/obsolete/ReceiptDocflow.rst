ReceiptDocflow
==============

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``ReceiptDocflow`` представляет собой информацию об извещении о получении (ИоП) документа.

.. code-block:: protobuf

   message ReceiptDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment ReceiptAttachment = 2;
   }

- ``IsFinished`` — признак того, что документооборот ИоП завершен. Принимает значение ``true`` в случае если ИоП имеет корректную подпись и на него было получено подтверждение оператора с корректной подписью.
- ``ReceiptAttachment`` — информация о файле извещения, представленная структурой :doc:`../SignedAttachment`.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`BilateralDocflow`,
	- в структуре :doc:`InboundInvoiceDocflow`,
	- в структуре :doc:`InboundUniversalTransferDocumentDocflow`,
	- в структуре :doc:`InvoiceConfirmationDocflow`,
	- в структуре :doc:`InvoiceCorrectionRequestDocflow`,
	- в структуре :doc:`OutboundInvoiceDocflow`,
	- в структуре :doc:`OutboundUniversalTransferDocumentDocflow`,
	- в структуре :doc:`UnilateralDocflow`,
	- в структуре :doc:`XmlBilateralDocflow`.

*Руководства:*
	- :doc:`../../Docflow API`