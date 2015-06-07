InvoiceCorrectionRequestDocflow
===============================

.. code-block:: protobuf

   message InvoiceCorrectionRequestDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment CorrectionRequestAttachment = 2;
       optional ReceiptDocflow ReceiptDocflow = 3;
   }

Структура представляет информацию об уведомлении об уточнении (УоУ) счёта-фактуры.

-  *IsFinished* - признак того, что документооборот УоУ завершен, т.е. уведомление имеет корректную подпись, и на него было получено извещение о получении с корректной подписью.
-  :doc:`CorrectionRequestAttachment <SignedAttachment>` - информация о файле УоУ.
-  :doc:`ReceiptDocflow` - информация об извещении о получении данного запроса.
