GetDocflowBatchRequest
======================

.. code-block:: protobuf

   message GetDocflowBatchRequest
   {
       repeated GetDocflowRequest Requests = 1;
   }

Структура представляет список запросов, передаваемых методу :doc:`../http/GetDocflows`. Максимальное количество запросов в структуре - 100.

-  :doc:`Requests <GetDocflowRequest>` - список запросов, по одному на документ.
