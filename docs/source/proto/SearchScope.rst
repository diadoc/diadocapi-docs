SearchScope
===========

.. code-block:: protobuf

    enum SearchScope
    {
        SearchScopeAny = 0;
        SearchScopeIncoming = 1;
        SearchScopeOutgoing = 2;
        SearchScopeDeleted = 3;
        SearchScopeInternal = 4;
    }

Задает область поиска метода :doc:`../http/SearchDocflows`.

-  *SearchScopeAny* - все документы в ящике.
-  *SearchScopeIncoming* - входящие.
-  *SearchScopeOutgoing* - исходящие.
-  *SearchScopeDeleted* - удаленные.
-  *SearchScopeInternal* - внутренние.
