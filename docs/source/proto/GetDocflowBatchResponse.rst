GetDocflowBatchResponse
=======================

.. code-block:: protobuf

   message GetDocflowBatchResponse
   {
       repeated DocumentWithDocflow Documents = 1;
   }

Структура представляет результат работы метода :doc:`../http/GetDocflows` - список документов с информацией о документообороте по каждому из них.

-  :doc:`Documents <DocumentWithDocflow>` - список документов.
