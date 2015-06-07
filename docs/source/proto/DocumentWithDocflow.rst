DocumentWithDocflow
===================

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

Структура представляет информацию о документе (метаданные и состояние документооборота), возвращаемую методами :doc:`../http/GetDocflows`, :doc:`../http/GetDocflowsByPacketId`, :doc:`../http/SearchDocflows`.

-  :doc:`DocumentId` - идентификатор документа.
-  *LastEventId* - идентификатор последнего события по документу, которое было учтено при формировании данной структуры.
-  :doc:`LastEventTimestamp <Timestamp>` - метка времени последнего события.
-  :doc:`DocumentInfo` - метаданные документа.
-  :doc:`Docflow` - информация о состоянии документооборота.
-  :doc:`InitialDocumentIds <DocumentId>` - идентификаторы документов, на которые ссылается данный документ.
-  :doc:`SubordinateDocumentIds <DocumentId>` - идентификаторы документов, которые ссылаются на данный документ.
-  :doc:`ForwardDocumentEvents <ForwardDocumentEvent>` - список событий по перемещению данного документа.
