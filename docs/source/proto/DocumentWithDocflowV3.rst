DocumentWithDocflowV3
=====================

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
        required EventId = 1;
        required Timestamp Timestamp = 2;
    }

Структура *DocumentWithDocflowV3* представляет информацию о документе (метаданные и состояние документооборота), возвращаемую методами :doc:`../http/GetDocflows_V3`, :doc:`../http/GetDocflowsByPacketId_V3`, :doc:`../http/SearchDocflows_V3`.

-  :doc:`DocumentId` - идентификатор документа.
-  *LastEvent* - информация о последнем событии в сообщении
-  :doc:`DocumentInfo <DocumentInfoV3>` - метаданные документа.
-  :doc:`Docflow <DocflowV3>` - информация о состоянии документооборота.

Структура *LastEvent* представляет информацию о последнего событии в сообщении

-  *EventId* - идентификатор последнего события в сообщении, которое было учтено при формировании данной структуры. Это событие может относиться и к другому документу из того же письма.
-  :doc:`Timestamp <Timestamp>` - метка времени последнего учтенного события.

