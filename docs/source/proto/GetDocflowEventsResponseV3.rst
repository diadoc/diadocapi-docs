GetDocflowEventsResponseV3
==========================

.. code-block:: protobuf

   message GetDocflowEventsResponse
   {
       optional int32 TotalCount = 1;
       repeated DocflowEventV3 Events = 2;
       required TotalCountType TotalCountType = 3;
   }

Структура представляет результат работы метода :doc:`../http/GetDocflowEvents_V3`.

-  *TotalCount* — количество всех событий, удовлетворяющих запросу.
-  :doc:`TotalCountType <TotalCountType>` — указано ли точное количество *TotalCount* или подсчет был ограничен соответствующим значением.
-  :doc:`Events <DocflowEventV3>` — список событий.
