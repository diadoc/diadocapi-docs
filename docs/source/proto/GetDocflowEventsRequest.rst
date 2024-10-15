GetDocflowEventsRequest
=======================

Структура ``GetDocflowEventsRequest`` представляет собой запрос на получение списка событий методом :doc:`../http/GetDocflowEvents_V3`.

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

- ``Filter`` — фильтр, задающий временные рамки, которым должны удовлетворять события. Представленный структурой :doc:`TimeBasedFilter`.
- ``AfterIndexKey`` — ключ для постраничного получения списка событий. Указывает на начало очередной страницы.
- ``PopulateDocuments`` — признак, указывающий, что в результат нужно включить полное состояние документа — метаданные и документооборот. По умолчанию имеет значение ``false``.
- ``InjectEntityContent`` — признак, указывающий, что в результат нужно включить содержимое документа. По умолчанию имеет значение ``false``.
- ``PopulatePreviousDocumentStates`` — признак, указывающий, что в результат нужно включить полное состояние документа на момент предыдущего события — метаданные и документооборот. Признак аналогичен ``PopulateDocuments`` и может быть установлен одновременно с ним. По умолчанию имеет значение ``false``.
- ``MessageTypes`` — список типов сообщения. Тип сообщения принимает значения:

	- ``Draft`` — черновик,
	- ``Letter`` — письмо,
	- ``Template`` — шаблон.

- ``DocumentDirections`` — список направлений документа относительно текущего ящика. Направление документа принимает значения:

	- ``Inbound`` — входящий,
	- ``Outbound`` — исходящий,
	- ``Internal`` — внутренний.

- ``DepartmentId`` — идентификатор подразделения, из которого нужно получить документы. Если параметр задан, то в результате вернутся события только по указанному подразделению. Может отсутствовать, если пользователь имеет доступ ко всем документам организации, иначе является обязательным. Можно указать любое подразделение, к документам которого пользователь имеет доступ.
- ``TypeNamedIds`` — список строковых идентификаторов типа документа.
- ``CounteragentBoxId`` — идентификатор ящика контрагента.
- ``Limit`` — максимальное количество событий в ответе. Принимает значения от 1 до 100. По умолчанию имеет значение 100.

----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/GetDocflowEvents_V3`