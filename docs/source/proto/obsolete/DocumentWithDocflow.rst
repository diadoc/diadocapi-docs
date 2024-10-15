DocumentWithDocflow
===================

.. warning::
	Структура устарела. Вместо нее используется структура :doc:`../DocumentWithDocflowV3`.

Структура ``DocumentWithDocflow`` представляет собой информацию о документе — метаданные и состояние документооборота.

.. code-block:: protobuf

   message DocumentWithDocflow
   {
       optional DocumentId DocumentId = 1;
       optional string LastEventId = 2;
       optional Timestamp LastEventTimestamp = 3;
       optional DocumentInfo DocumentInfo = 4;
       optional Docflow Docflow = 5;
       repeated DocumentId InitialDocumentIds = 6;
       repeated DocumentId SubordinateDocumentIds = 7;
       repeated ForwardDocumentEvent ForwardDocumentEvents = 8;
   }

- ``DocumentId`` — идентификатор документа, представленный структурой :doc:`../DocumentId`.
- ``LastEventId`` — идентификатор последнего события в письме, которое было учтено при формировании данной структуры. Это событие может относиться и к другому документу из того же письма.
- ``LastEventTimestamp`` — время последнего учтенного события, представленное структурой :doc:`../Timestamp`.
- ``DocumentInfo`` — метаданные документа, представленные структурой :doc:`DocumentInfo`.
- ``Docflow`` — информация о состоянии документооборота, представленная структурой :doc:`Docflow`.
- ``InitialDocumentIds`` — идентификаторы документов, на которые ссылается данный документ, представленные структурой :doc:`../DocumentId`.
- ``SubordinateDocumentIds`` — идентификаторы документов, которые ссылаются на данный документ, представленные структурой :doc:`../DocumentId`.
- ``ForwardDocumentEvents`` — события по перемещению данного документа, представленные структурой :doc:`../ForwardDocumentEvent`.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`../ForwardedDocument`
	- в устаревшей структуре :doc:`DocflowEvent`
	- в устаревшей структуре :doc:`FetchedDocument`
	- в устаревшей структуре :doc:`GetDocflowBatchResponse`
	- в устаревшей структуре :doc:`SearchDocflowsResponse`