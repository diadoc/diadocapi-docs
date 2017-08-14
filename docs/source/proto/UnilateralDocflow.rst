UnilateralDocflow
=================

.. code-block:: protobuf

   message UnilateralDocflow
   {
       optional bool IsFinished = 1;
       optional ReceiptDocflow ReceiptDocflow = 2;
       optional bool IsReceiptRequested = 3;
       optional bool CanDocumentBeReceipted = 4;
       optional bool CanDocumentBeSignedBySender = 5;
   }

Структура представляет информацию о документообороте одностороннего неформализованного документа.

-  *IsFinished* - признак того, что документооборот завершен, т.е. документ не требует дальнейших действий.
-  :doc:`ReceiptDocflow` - информация об извещении о получении на данный документ.
-  *IsReceiptRequested* - признак того, что по документу было запрошено извещение о получении.
-  *CanDocumentBeReceipted* - признак того, что для документа можно отправить извещение о получении. Равен true для входящих документов, по которым корректные извещения ранее не отправлялись.
-  *CanDocumentBeSignedBySender* - признак того, что документ может быть подписан отправителем. Равен true для документов, сохраненных для последующей отправки, либо для исходящих документов с некорректной подписью.
