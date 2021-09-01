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
       repeated string MessageTypes = 6;
       repeated string DocumentDirections = 7;
       optional string DepartmentId = 8;
       repeated string TypeNamedIds = 9;
       optional string CounteragentBoxId = 10;
       optional int32 Limit = 11 [default = 100];
   }

Структура представляет запрос, передаваемый методу :doc:`../http/GetDocflowEvents`.

-  :doc:`Filter <TimeBasedFilter>` - фильтр, позволяющий указать временные рамки, которым должны удовлетворять события.
-  *AfterIndexKey* - ключ, используемый для постраничной выгрузки. Указывает на начало очередной выгружаемой страницы.
-  *PopulateDocuments* - признак того, что в выдачу нужно включить полное состояние документа (метаданные и документооборот).
-  *PopulatePreviousDocumentStates* - признак, аналогичный *PopulateDocuments*, может быть установлен одновременно с ним. Указывает, что в выдачу нужно дополнительно включить полное состояние документа на момент возникновения предыдущего события.
- *MessageType* - тип сообщения: черновик (Draft), письмо (Letter), шаблон (Template).
- *DocumentDirection* - направление документа относительно данного ящика: входящий (Inbound), исходящий (Outbound), внутренний (Internal).
- *DepartmentId* - идентификатор подразделения, из которого производится выборка документов. Параметр может отсутствовать, если пользователь имеет доступ ко всем документам организации. Пользователям с ограниченным доступом необходимо задать параметр. Указать можно любое подразделение, к документам которого пользователь имеет доступ. Если параметр задан, вернутся события только по указанному подразделению.
- *TypeNamedId* - строковый идентификатор типа документа, возможно указание нескольких идентификаторов.
- *CounteragentBoxId* - идентификатор ящика контрагента.
- *Limit* - максимальное количество документов в ответе (может отсутствовать, в этом случае в ответе будет не больше 100 документов). Может принимать значения от 1 до 100.