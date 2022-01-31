DepartmentList
==============

.. code-block:: protobuf

    message DepartmentList
    {
        repeated Department Departments = 1;
        required int32 TotalCount = 2; // Общее кол-во подразделений
    }

Структура ``DepartmentList`` содержит список подразделений.

- :doc:`Departments <Department>` - список запрошенных подразделений.
- ``TotalCount`` - общее кол-во подразделений.