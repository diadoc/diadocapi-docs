EmployeeList
============

Структура ``EmployeeList`` представляет собой список сотрудников.

.. code-block:: protobuf

    message EmployeeList {
        repeated Employee Employees = 1;
        required int32 TotalCount = 2;
    }

- ``Employees`` — список сотрудников, представленных структурой :doc:`Employees <Employee>`.
- ``TotalCount`` — общее количество сотрудников в организации, удовлетворяющих запросу.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetEmployees`