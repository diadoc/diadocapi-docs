ReceiptDocflow
==============

.. warning::
	Структура устарела.

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
	- в устаревшей структуре :doc:`BilateralDocflow`
	- в устаревшей структуре :doc:`InboundInvoiceDocflow`
	- в устаревшей структуре :doc:`InboundUniversalTransferDocumentDocflow`
	- в устаревшей структуре :doc:`InvoiceConfirmationDocflow`
	- в устаревшей структуре :doc:`InvoiceCorrectionRequestDocflow`
	- в устаревшей структуре :doc:`OutboundInvoiceDocflow`
	- в устаревшей структуре :doc:`OutboundUniversalTransferDocumentDocflow`
	- в устаревшей структуре :doc:`UnilateralDocflow`
	- в устаревшей структуре :doc:`XmlBilateralDocflow`