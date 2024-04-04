UnilateralDocflow
=================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``UnilateralDocflow`` представляет собой информацию о документообороте одностороннего неформализованного документа.

.. code-block:: protobuf

   message UnilateralDocflow
   {
       optional bool IsFinished = 1;
       optional ReceiptDocflow ReceiptDocflow = 2;
       optional bool IsReceiptRequested = 3;
       optional bool CanDocumentBeReceipted = 4;
       optional bool CanDocumentBeSignedBySender = 5;
   }

- ``IsFinished`` — признак того, что документооборот завершен и документ не требует дальнейших действий.
- ``ReceiptDocflow`` — информация об извещении о получении на данный документ, представленная структурой :doc:`ReceiptDocflow`.
- ``IsReceiptRequested`` — признак того, что по документу было запрошено извещение о получении.
- ``CanDocumentBeReceipted`` — признак того, что для документа можно отправить извещение о получении. Принимает значение ``true`` для входящих документов, по которым корректные извещения ранее не отправлялись.
- ``CanDocumentBeSignedBySender`` — признак того, что документ может быть подписан отправителем. Принимает значение ``true`` для документов, сохраненных для последующей отправки, либо для исходящих документов с некорректной подписью.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Docflow`.

*Руководства:*
	- :doc:`../../Docflow API`