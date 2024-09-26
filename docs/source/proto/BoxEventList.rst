BoxEventList
============

Структура ``BoxEventList`` представляет собой список событий в :doc:`ящике<../entities/box>`.

.. code-block:: protobuf

    message BoxEventList {
        repeated BoxEvent Events = 1;
        optional int32 TotalCount = 2;
        required TotalCountType TotalCountType = 3;
    }

- ``Events`` — список событий в ящике. Каждый элемент списка представлен структурой :doc:`BoxEvent`.
- ``TotalCount`` — общее количество событий, удовлетворяющих запросу.
- ``TotalCountType`` — параметр, указывающий, является ли значение ``TotalCount`` точным или подсчет был ограничен. Принимает значения из перечисления :doc:`TotalCountType`.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetNewEvents`
