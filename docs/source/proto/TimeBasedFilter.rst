TimeBasedFilter
===============

Структура ``TimeBasedFilter`` представляет собой фильтр, позволяющий ограничить по времени возвращаемые методом :doc:`../http/GetDocflowEvents_V3` события и указать порядок их сортировки.

.. code-block:: protobuf

   message TimeBasedFilter
   {
       optional Timestamp FromTimestamp = 1;
       optional Timestamp ToTimestamp = 2;
       optional SortDirection SortDirection = 3 [default = Ascending];
   }

- ``FromTimestamp`` — нижняя граница времени, представленная структурой :doc:`Timestamp`.
- ``ToTimestamp`` — верхняя граница времени, представленная структурой :doc:`Timestamp`.
- ``SortDirection`` — порядок сортировки событий, представленный структурой :doc:`SortDirection`.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`GetDocflowEventsRequest`,
	- в структуре ``GetForwardedDocumentEventsRequest``, передаваемой в теле запроса метода :doc:`../http/GetForwardedDocumentEvents`.