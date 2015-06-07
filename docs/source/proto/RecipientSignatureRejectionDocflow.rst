RecipientSignatureRejectionDocflow
==================================

.. code-block:: protobuf

   message RecipientSignatureRejectionDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment RecipientSignatureRejectionAttachment = 2;
       optional Timestamp DeliveryTimestamp = 3;
   }

Структура представляет информацию об отказе контрагента в подписании документа. Отказ является подписанным файлом установленного формата.

-  *IsFinished* - признак того, что документооборот по отказу завершен. Равен true в том случае, когда подпись под отказом проверена, и он доставлен контрагенту.
-  :doc:`RecipientSignatureRejectionAttachment <SignedAttachment>` - информация о файле отказа.
-  :doc:`DeliveryTimestamp <Timestamp>` - метка времени доставки отказа.
