DocflowEvent
============

.. code-block:: protobuf

   message DocflowEvent
   {
       optional string EventId = 1;
       optional Timestamp Timestamp = 2;
       optional DocumentId DocumentId = 3;
       optional bytes IndexKey = 4;
       optional DocumentWithDocflow Document = 5;
       optional string PreviousEventId = 6;
       optional DocumentWithDocflow PreviousDocumentState = 7;
   }

Структура представляет одно событие, возвращаемое методом :doc:`../http/GetDocflowEvents`.

-  *EventId* - идентификатор события.

-  :doc:`Timestamp` - метка времени возникновения события.

-  :doc:`DocumentId` - идентификатор документа, с которым произошло событие.

-  *IndexKey* - ключ события. Используется для постраничной выгрузки и позволяет указать, с какого события выгружать очередную страницу.

-  :doc:`Document <DocumentWithDocflow>` - полное состояние документа после возникновения данного события.

-  *PreviousEventId* - идентификатор предыдущего события по данному документу.

-  :doc:`PreviousDocumentState <DocumentWithDocflow>` - полное состояние документа после возникновения предыдущего события (т.е. до возникновения данного события). 

Сравнивая содержимое полей *Document* и *PreviousDocumentState*, можно составить картину изменений, которые произошли с документом.