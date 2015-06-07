SearchDocflowsRequest
=====================

.. code-block:: protobuf

   message SearchDocflowsRequest
   {
       required string QueryString = 1;
       optional int32 Count = 2 [default = 100];
       optional int32 FirstIndex = 3;
       optional SearchScope Scope = 4 [default = SearchScopeAny];
       optional bool InjectEntityContent = 5 [default = false];
   }

Представляет запрос, передаваемый методу :doc:`../http/SearchDocflows`.

-  *QueryString* - строка запроса. Может иметь либо произвольное значение, либо строку в формате (YAML) "key: value".
-  *Count* - максимальное количество документов в выдаче, не должно превышать 100.
-  *FirstIndex* - индекс документа, с которого нужно начинать выгрузку. Используется для постраничной выгрузки документов, когда их общее количество превышает допустимый размер выдачи.
-  :doc:`Scope <SearchScope>` - область действия поиска.
-  *InjectEntityContent* - признак того, что в выдачу нужно включать содержимое документов.
