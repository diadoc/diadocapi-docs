SortDirection
=============

.. code-block:: protobuf

    enum SortDirection
    {
        UnknownSortDirection = 0;
        Ascending = 1;
        Descending = 2;
    }

Порядок сортировки событий по метке времени в выдаче метода :doc:`../http/GetDocflowEvents`. Указывается передачей в метод фильтра :doc:`TimeBasedFilter`.

-  *UnknownSortDirection* - зарезервировано.
-  *Ascending* - порядок по возрастанию.
-  *Descending* - порядок по убыванию.
