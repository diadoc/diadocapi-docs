GetDocflowBatchResponseV3
=========================

.. code-block:: protobuf

   message GetDocflowBatchResponseV3
   {
       repeated DocumentWithDocflowV3 Documents = 1;
   }

Структура представляет результат работы метода :doc:`../http/GetDocflows_V3` - список документов с информацией о документообороте по каждому из них.

-  :doc:`Documents <DocumentWithDocflowV3>` - список документов.
