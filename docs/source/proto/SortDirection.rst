SortDirection
=============

Перечисление ``SortDirection`` представляет собой порядок сортировки событий по метке времени в ответе метода :doc:`../http/GetDocflowEvents_V3`.

.. code-block:: protobuf

    enum SortDirection
    {
        UnknownSortDirection = 0;
        Ascending = 1;
        Descending = 2;
    }

- ``UnknownSortDirection`` — зарезервировано.
- ``Ascending`` — порядок по возрастанию.
- ``Descending`` — порядок по убыванию.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`TimeBasedFilter`.