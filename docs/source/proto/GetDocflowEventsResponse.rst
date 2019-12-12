GetDocflowEventsResponse
========================

.. code-block:: protobuf

   message GetDocflowEventsResponse
   {
       optional int32 TotalCount = 1;
       repeated DocflowEvent Events = 2;
       required TotalCountType TotalCountType = 3;
   }

Структура представляет результат работы метода :doc:`../http/GetDocflowEvents`.

-  *TotalCount* — количество всех событий, удовлетворяющих запросу.
-  :doc:`TotalCountType <TotalCountType>` — указано ли точное количество *TotalCount* или подсчет был ограничен соответствующим значением.
-  :doc:`Events <DocflowEvent>` — список событий.
