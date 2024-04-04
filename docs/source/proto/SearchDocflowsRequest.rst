SearchDocflowsRequest
=====================

Структура ``SearchDocflowsRequest`` представляет собой запрос для поиска документов методом :doc:`../http/SearchDocflows_V3`.

.. code-block:: protobuf

   message SearchDocflowsRequest
   {
       required string QueryString = 1;
       optional int32 Count = 2 [default = 100];
       optional int32 FirstIndex = 3;
       optional SearchScope Scope = 4 [default = SearchScopeAny];
       optional bool InjectEntityContent = 5 [default = false];
   }

- ``QueryString`` — строка запроса. Принимает значения:
	
	- произвольная строка поиска, представляющая собой токены, разделенные пробелами или разделительными символами;
	- строку в формате YAML вида «ключ: значение».
	
- ``Count`` — максимальное количество документов в выдаче, не должно превышать 100.
- ``FirstIndex`` — индекс документа, с которого начинается страница. Используется для постраничного получения документов, если их количество в результате поиска превышает максимальное значение в 100 элементов. 
- ``Scope`` — область действия поиска, представленная перечислением :doc:`SearchScope`.
- ``InjectEntityContent`` — признак того, что в результат поиска нужно включить содержимое документов.

----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/SearchDocflows_V3`