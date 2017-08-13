XmlBilateralDocflow
===================

.. code-block:: protobuf

   message XmlBilateralDocflow
   {
       optional bool IsFinished = 1;
       optional ReceiptDocflow ReceiptDocflow = 2;
       optional BuyerTitleDocflow BuyerTitleDocflow = 3;
       optional RecipientSignatureRejectionDocflow RecipientSignatureRejectionDocflow = 4;
       optional bool IsReceiptRequested = 5;
       optional bool IsDocumentSignedByRecipient = 6;
       optional bool IsDocumentRejectedByRecipient = 7;
       optional bool CanDocumentBeReceipted = 8;
       optional bool CanDocumentBeSignedBySender = 9;
       optional bool CanDocumentBeSignedOrRejectedByRecipient = 10;
   }

Структура представляет информацию о документообороте двустороннего формализованного документа.

-  *IsFinished* - признак того, что документооборот завершен, т.е. документ не требует каких-либо действий со стороны отправители или получателя.

-  :doc:`ReceiptDocflow` - информация об извещении о получении на данный документ.

-  :doc:`BuyerTitleDocflow` - информация об ответной подписи под документом. Ответная подпись для формализованных двусторонних документов представляет собой подписанный файл установленного формата (например, титул покупателя для товарной накладной, или титул заказчика для акта).

-  :doc:`RecipientSignatureRejectionDocflow` - информация об отказе в подписании документа получателем. Заполняется только в том случае, когда отказ был.

-  *IsReceiptRequested* - признак того, что по документу было запрошено извещение о получении.

-  *IsDocumentSignedByRecipient* - признак того, что документ подписан получателем.

-  *IsDocumentRejectedByRecipient* - признак того, что получатель отказал в подписи документа.

-  *CanDocumentBeReceipted* - признак того, что для документа можно отправить извещение о получении. Равен true для входящих документов, по которым корректные извещения ранее не отправлялись.

-  *CanDocumentBeSignedBySender* - признак того, что документ может быть подписан отправителем. Равен true для документов, сохраненных для последующей отправки, либо для исходящих документов с некорректной подписью.

-  *CanDocumentBeSignedOrRejectedByRecipient* - признак того, что получатель может подписать документ или отказать в подписании.
