GetDocflowEventsResponse
========================

.. warning::
	Структура относится к устаревшей версии Docflow API. Вместо нее используется структура :doc:`../../proto/GetDocflowEventsResponseV3` последней версии :doc:`../../Docflow API` — V3.

Структура ``GetDocflowEventsResponse`` представляет собой список событий, полученных методом :doc:`../../http/obsolete/GetDocflowEvents`.

.. code-block:: protobuf

   message GetDocflowEventsResponse
   {
       optional int32 TotalCount = 1;
       repeated DocflowEvent Events = 2;
       required TotalCountType TotalCountType = 3;
   }

- ``TotalCount`` — количество всех событий, удовлетворяющих запросу.
- ``Events`` — список событий, представленных структурой :doc:`DocflowEvent`.
- ``TotalCountType`` — параметр, указывающий, является ли значение ``TotalCount`` точным или подсчет был ограничен. Представлен структурой :doc:`../TotalCountType`.

----

.. rubric:: Смотри также

*Структура используется:*
	- в теле ответа метода :doc:`../../http/obsolete/GetDocflowEvents`.

*Руководства:*
	- :doc:`../../Docflow API`