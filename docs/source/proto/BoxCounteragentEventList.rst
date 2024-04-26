BoxCounteragentEventList
========================

Структура ``BoxCounteragentEventList`` представляет собой список событий по изменению отношений с :doc:`контрагентами <../entities/counteragent>`.

.. code-block:: protobuf

   message BoxCounteragentEventList {
        repeated BoxCounteragentEvent Events = 1;
        optional int32 TotalCount = 2;
        required TotalCountType TotalCountType = 3;
    }

    message BoxCounteragentEvent {
        required string EventId = 1;
        optional CounteragentInfo Counteragent = 2;
        optional string IndexKey = 3;
    }

- ``Events`` — список событий по изменению отношений с контрагентами. Каждое событие представлено структурой ``BoxCounteragentEvent`` с полями:

	- ``EventId`` — идентификатор события.
	- ``Counteragent`` — информация о контрагенте, представленная структурой :doc:`../proto/CounteragentInfo`.
	- ``IndexKey`` — ключ события, который можно передавать в качестве параметра ``afterIndexKey`` для итерирования по отфильтрованному списку.

- ``TotalCount`` — количество событий, удовлетворяющих запросу.
- ``TotalCountType`` — параметр, указывающий, является ли значение ``TotalCount`` точным или подсчет был ограничен. Принимает значения из перечисления :doc:`../proto/TotalCountType`.

----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetCounteragentEvents`