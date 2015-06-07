BuyerTitleDocflow
=================

.. code-block:: protobuf

   message BuyerTitleDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment BuyerTitleAttachment = 2;
       optional Timestamp SendTimestamp = 3;
       optional Timestamp DeliveryTimestamp = 4;
   }

Структура представляет информацию об ответной подписи под двусторонним формализованным документом (титул покупателя). Ответная подпись в этом случае является подписанным формализованным файлом установленного формата.

-  *IsFinished* - признак того, что документооборот ответной подписи завершен. Равен true в том случае, когда подпись под титулом покупателя проверена, и он доставлен контрагенту.
-  :doc:`BuyerTitleAttachment <SignedAttachment>` - информация о файле титула покупателя.
-  :doc:`SendTimestamp <Timestamp>` - метка времени отправки титула покупателя.
-  :doc:`DeliveryTimestamp <Timestamp>` - метка времени доставки титула покупателя.
