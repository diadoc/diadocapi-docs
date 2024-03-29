BilateralDocflow
================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``BilateralDocflow`` представляет собой информацию о документообороте двустороннего неформализованного документа.

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

- ``IsFinished`` — признак того, что документооборот завершен и документ не требует дальнейших действий.
- ``ReceiptDocflow`` — информация об извещении о получении на данный документ, представленная структурой :doc:`ReceiptDocflow`.
- ``RecipientSignatureDocflow`` — информация об ответной подписи под документом, представленная структурой :doc:`RecipientSignatureDocflow`.
- ``RecipientSignatureRejectionDocflow`` — информация об отказе в подписании документа получателем, представленная структурой :doc:`RecipientSignatureRejectionDocflow`. Заполняется только если отказ был.
- ``IsReceiptRequested`` — признак того, что по документу было запрошено извещение о получении.
- ``IsRecipientSignatureRequested`` — признак того, что по документу запрошена ответная подпись.
- ``IsDocumentSignedByRecipient`` — признак того, что документ подписан получателем.
- ``IsDocumentRejectedByRecipient`` — признак того, что получатель отказал в подписи документа.
- ``CanDocumentBeReceipted`` — признак того, что для документа можно отправить извещение о получении. Принимает значение ``true`` для входящих документов, по которым корректные извещения ранее не отправлялись.
- ``CanDocumentBeSignedBySender`` — признак того, что документ может быть подписан отправителем. Принимает значение ``true`` для документов, сохраненных для последующей отправки, либо для исходящих документов с некорректной подписью.
- ``CanDocumentBeSignedOrRejectedByRecipient`` — признак того, что получатель может подписать документ или отказать в подписании.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`Docflow`.

*Руководства:*
	- :doc:`../../Docflow API`