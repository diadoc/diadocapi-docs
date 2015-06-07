BilateralDocflow
================

.. code-block:: protobuf

   message BilateralDocflow
   {
       optional bool IsFinished = 1;
       optional ReceiptDocflow ReceiptDocflow = 2;
       optional RecipientSignatureDocflow RecipientSignatureDocflow = 3;
       optional RecipientSignatureRejectionDocflow RecipientSignatureRejectionDocflow = 4;
       optional bool IsReceiptRequested = 5;
       optional bool IsRecipientSignatureRequested = 6;
       optional bool IsDocumentSignedByRecipient = 7;
       optional bool IsDocumentRejectedByRecipient = 8;
       optional bool CanDocumentBeReceipted = 9;
       optional bool CanDocumentBeSignedBySender = 10;
       optional bool CanDocumentBeSignedOrRejectedByRecipient = 11;
   }

Структура представляет информацию о документообороте двустороннего неформализованного документа.

-  *IsFinished* - признак того, что документооборот завершен, т.е. документ не требует каких-либо действий со стороны отправители или получателя.
-  :doc:`ReceiptDocflow` - информация об извещении о получении на данный документ.
-  :doc:`RecipientSignatureDocflow` - информация об ответной подписи под документом.
-  :doc:`RecipientSignatureRejectionDocflow` - информация об отказе в подписании документа получателем. Заполняется только в том случае, когда отказ был.
-  *IsReceiptRequested* - признак того, что по документу было запрошено извещение о получении.
-  *IsRecipientSignatureRequested* - признак того, что по документу запрошена ответная подпись.
-  *IsDocumentSignedByRecipient* - признак того, что документ подписан получателем.
-  *IsDocumentRejectedByRecipient* - признак того, что получатель отказал в подписи документа.
-  *CanDocumentBeReceipted* - признак того, что для документа можн отправить извещение о получении. Равен true для входящих документов, по которым корректные извещения ранее не отправлялись.
-  *CanDocumentBeSignedBySender* - признак того, что документ может быть подписан отправителем. Равен true для документов, сохраненных для последующий отправки, либо для исходящих документов с некорректной подписью.
-  *CanDocumentBeSignedOrRejectedByRecipient* - признак того, что получатель может подписать документ или отказать в подписании.