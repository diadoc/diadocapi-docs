SearchDocflowsResponse
======================

.. code-block:: protobuf

   message SearchDocflowsResponse
   {
       repeated DocumentWithDocflow Documents = 1;
       optional bool HaveMoreDocuments = 2;
   }

Представляет результат работы метода :doc:`../http/SearchDocflows`.

-  :doc:`Documents <DocumentWithDocflow>` - список документов.
-  *HaveMoreDocuments* - признак того, что условиям поиска соответствует больше документов, чем было возвращено. Остальные документы можно выгрузить постранично, передавая в запросе индекс первого документа очередной страницы (см. пример использования :doc:`../http/SearchDocflows`).
