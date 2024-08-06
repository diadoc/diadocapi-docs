InboundInvoiceReceiptDocflow
============================

.. warning::
	Структура устарела.

Структура ``InboundInvoiceReceiptDocflow`` представляет собой информацию об извещении о получении (ИоП) в рамках документооборота входящего счета-фактуры.

.. code-block:: protobuf

   message InboundInvoiceReceiptDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment ReceiptAttachment = 2;
       optional InvoiceConfirmationDocflow ConfirmationDocflow = 3;
   }

- ``IsFinished`` — признак того, что документооборот ИоП завершен. Принимает значение ``true`` в случае если ИоП имеет корректную подпись и на него было получено подтверждение оператора с корректной подписью.
- ``ReceiptAttachment`` — информация о файле ИоП, представленная структурой :ref:`ReceiptAttachment`.
- ``ConfirmationDocflow`` — информация о подтверждении оператора на данное ИоП, представленная структурой :doc:`InvoiceConfirmationDocflow`.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`InboundInvoiceDocflow`
	- в устаревшей структуре :doc:`InboundUniversalTransferDocumentDocflow`