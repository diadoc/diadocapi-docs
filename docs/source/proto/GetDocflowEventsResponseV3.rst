GetDocflowEventsResponseV3
==========================

.. code-block:: protobuf

   message GetDocflowEventsResponse
   {
       optional int32 TotalCount = 1;
       repeated DocflowEventV3 Events = 2;
   }

Структура представляет результат работы метода :doc:`../http/GetDocflowEvents_V3`.

-  *TotalCount* - количество всех событий, удовлетворяющих запросу.
-  :doc:`Events <DocflowEventV3>` - список событий.
