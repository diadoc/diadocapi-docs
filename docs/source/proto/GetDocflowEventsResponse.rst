GetDocflowEventsResponse
========================

.. code-block:: protobuf

   message GetDocflowEventsResponse
   {
       optional int32 TotalCount = 1;
       repeated DocflowEvent Events = 2;
   }

Структура представляет результат работы метода :doc:`../http/GetDocflowEvents`.

-  *TotalCount* - количество всех событий, удовлетворяющих запросу.
-  :doc:`Events <DocflowEvent>` - список событий.
