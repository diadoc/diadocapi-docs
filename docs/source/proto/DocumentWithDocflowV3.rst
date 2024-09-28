DocumentWithDocflowV3
=====================

Структура ``DocumentWithDocflowV3`` хранит информацию о документе — метаданные и состояние документооборота.

.. code-block:: protobuf

    message DocumentWithDocflowV3
    {
        required DocumentId DocumentId = 1;
        required LastEvent LastEvent = 2;
        required DocumentInfoV3 DocumentInfo = 3;
        required DocflowV3 Docflow = 4;
    }

    message LastEvent
    {
        required string EventId = 1;
        required Timestamp Timestamp = 2;
    }

- ``DocumentId`` — идентификатор документа, представленный структурой :doc:`DocumentId`.
- ``LastEvent`` — информация о последнем событии в сообщении, представленная структурой ``LastEvent`` с полями:

	- ``EventId`` — идентификатор последнего события в сообщении, которое было учтено при формировании данной структуры. Это событие может относиться к другому документу из того же сообщения.
	- ``Timestamp`` — время последнего учтенного события, представленное структурой :doc:`Timestamp`.

- ``DocumentInfo`` — метаданные документа, представленные структурой :doc:`DocumentInfoV3`.
- ``Docflow`` — информация о состоянии документооборота, представленная структурой :doc:`DocflowV3`.



----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocflowEventV3`
	- в структуре :doc:`FetchedDocumentV3`
	- в структуре :doc:`GetDocflowBatchResponseV3`
	- в структуре :doc:`SearchDocflowsResponseV3`