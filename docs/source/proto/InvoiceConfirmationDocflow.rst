InvoiceConfirmationDocflow
==========================

.. code-block:: protobuf

   message InvoiceConfirmationDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment ConfirmationAttachment = 2;
       optional ReceiptDocflow ReceiptDocflow = 3;
   }

Структура представляет информацию о подтверждении оператора в рамках документооборота счёта-фактуры.

-  *IsFinished* - признак того, что документооборот подтверждения завершен. Значение true говорит о том, что подтверждение имеет корректную подпись, и оператором в ответ на это подтверждение было получено извещение о получении с корректной подписью.
-  :doc:`ConfirmationAttachment <SignedAttachment>` - информация о файле подтверждения.
-  :doc:`ReceiptDocflow` - информация об извещении о получении данного подтверждения.
