SearchScope
===========

Перечисление ``SearchScope`` задает область поиска метода :doc:`../http/SearchDocflows_V3`.

.. code-block:: protobuf

    enum SearchScope
    {
        SearchScopeAny = 0;
        SearchScopeIncoming = 1;
        SearchScopeOutgoing = 2;
        SearchScopeDeleted = 3;
        SearchScopeInternal = 4;
    }

- ``SearchScopeAny`` — все документы в ящике.
- ``SearchScopeIncoming`` — входящие.
- ``SearchScopeOutgoing`` — исходящие.
- ``SearchScopeDeleted`` — удаленные.
- ``SearchScopeInternal`` — внутренние.

----

.. rubric:: Смотри также

*Перечисление используется:*
	- в структуре :doc:`SearchDocflowsRequest`.