GetDocflowEventsRequest
=======================

.. code-block:: protobuf

   message GetDocflowEventsRequest
   {
       required TimeBasedFilter Filter = 1;
       optional bytes AfterIndexKey = 2;
       optional bool PopulateDocuments = 3 [default = false];
       optional bool InjectEntityContent = 4 [default = false];
       optional bool PopulatePreviousDocumentStates = 5 [default = false];
   }

Структура представляет запрос, передаваемый методу :doc:`../http/GetDocflowEvents`.

-  :doc:`Filter <TimeBasedFilter>` - фильтр, позволяющий указать временные рамки, которым должны удовлетворять события.
-  *AfterIndexKey* - ключ, используемый для постраничной выгрузки. Указывает на начало очередной выгружаемой страницы.
-  *PopulateDocuments* - признак того, что в выдачу нужно включить полное состояние документа (метаданные и документооборот).
-  *PopulatePreviousDocumentStates* - признак, аналогичный *PopulateDocuments*, может быть установлен одновременно с ним. Указывает, что в выдачу нужно дополнительно включить полное состояние документа на момент возникновения предыдущего события.
