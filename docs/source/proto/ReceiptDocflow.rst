ReceiptDocflow
==============

.. code-block:: protobuf

   message ReceiptDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment ReceiptAttachment = 2;
   }

Структура представляет информацию об извещении о получении (ИоП) документа.

-  *IsFinished* - признак того, что документооборот ИоП завершен. Значение true говорит о том, что ИоП имеет корректную подпись, и на него было получено подтверждение оператора с корректной подписью.
-  :doc:`ReceiptAttachment <SignedAttachment>` - информация о файле извещения.
