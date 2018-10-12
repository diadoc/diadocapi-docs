EmployeeList
============

.. code-block:: protobuf

    message EmployeeList {
        repeated Employee Employees = 1;
        required int32 TotalCount = 2;
    }

Структура содержит список сотрудников организации. Возвращается методом :doc:`../http/GetEmployees`.

 - :doc:`Employees <Employee>` - список сотрудников. Содержит одну страницу из полного списка сотрудников
 - *TotalCount* - общее количество сотрудников в организации
