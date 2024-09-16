DocflowEventV3
==============

Структура ``DocflowEventV3`` представляет собой событие, возвращаемое методом :doc:`../http/GetDocflowEvents_V3`.

.. code-block:: protobuf

    message DocflowEventV3
    {
        optional string EventId = 1;
        optional Timestamp Timestamp = 2;
        optional DocumentId DocumentId = 3;
        optional bytes IndexKey = 4;
        optional DocumentWithDocflowV3 Document = 5;
        optional string PreviousEventId = 6;
        optional DocumentWithDocflowV3 PreviousDocumentState = 7;
    }

- ``EventId`` — идентификатор события.
- ``Timestamp`` — время возникновения события, представленное структурой :doc:`Timestamp`.
- ``DocumentId`` — идентификатор документа, с которым произошло событие, представленный структурой :doc:`DocumentId`.
- ``IndexKey`` — ключ события. Используется для постраничной выгрузки событий; позволяет указать, с какого события выгружать очередную страницу.
- ``Document`` — полное состояние документа после возникновения данного события, представленное структурой :doc:`DocumentWithDocflowV3`.
- ``PreviousEventId`` — идентификатор предыдущего события по текущему документу.
- ``PreviousDocumentState`` - полное состояние документа после возникновения предыдущего события — до возникновения данного события, представленное стурктурой :doc:`DocumentWithDocflowV3`. 

Чтобы узнать изменения, произошедшие с документом в связи с данным событием, нужно сравнить значения полей ``Document`` и ``PreviousDocumentState``.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`GetDocflowEventsResponseV3`