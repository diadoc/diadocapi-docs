SearchDocflowsResponseV3
========================

.. code-block:: protobuf

   message SearchDocflowsResponseV3
   {
       repeated DocumentWithDocflowV3 Documents = 1;
       optional bool HaveMoreDocuments = 2;
   }

Представляет результат работы метода :doc:`../http/SearchDocflows_V3`.

-  :doc:`Documents <DocumentWithDocflowV3>` - список документов.
-  *HaveMoreDocuments* - признак того, что условиям поиска соответствует больше документов, чем было возвращено. Остальные документы можно выгрузить постранично, передавая в запросе индекс первого документа очередной страницы (см. пример использования :doc:`../http/SearchDocflows_V3`).
