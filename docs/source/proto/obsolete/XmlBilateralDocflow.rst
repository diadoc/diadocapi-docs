XmlBilateralDocflow
===================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``XmlBilateralDocflow`` представляет собой информацию о документообороте двустороннего формализованного документа.

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

- ``IsFinished`` — признак того, что документооборот завершен и документ не требует дальнейших действий.
- ``ReceiptDocflow`` — информация об извещении о получении на данный документ, представленный структурой :doc:`ReceiptDocflow`.
- ``BuyerTitleDocflow`` — информация об ответной подписи под документом, представленный структурой :doc:`BuyerTitleDocflow`. Ответная подпись для формализованных двусторонних документов представляет собой подписанный файл установленного формата: например, титул покупателя для товарной накладной или титул заказчика для акта.
- ``RecipientSignatureRejectionDocflow`` — информация об отказе в подписании документа получателем, представленная структурой :doc:`RecipientSignatureRejectionDocflow`. Заполняется только в случае если отказ был.
- ``IsReceiptRequested`` — признак того, что по документу было запрошено извещение о получении.
- ``IsDocumentSignedByRecipient`` — признак того, что документ подписан получателем.
- ``IsDocumentRejectedByRecipient`` — признак того, что получатель отказал в подписи документа.
- ``CanDocumentBeReceipted`` — признак того, что для документа можно отправить извещение о получении. Принимает значение ``true`` для входящих документов, по которым корректные извещения ранее не отправлялись.
- ``CanDocumentBeSignedBySender`` — признак того, что документ может быть подписан отправителем. Принимает значение ``true`` для документов, сохраненных для последующей отправки, либо для исходящих документов с некорректной подписью.
- ``CanDocumentBeSignedOrRejectedByRecipient`` — признак того, что получатель может подписать документ или отказать в подписании.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Docflow`