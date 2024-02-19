CounteragentGroup
=================

Структура ``CounteragentGroup`` представляет собой группу контрагентов.

.. code-block:: protobuf

    message CounteragentGroup {
        required string CounteragentGroupId = 1;
        required string Name = 2;
        optional DepartmentsInGroup Departments = 3;
    }

     message DepartmentsInGroup {
        repeated string DepartmentId = 1;
    }

- ``CounteragentGroupId`` — идентификатор группы контрагентов.
- ``Name`` — наименование группы контрагентов.
- ``Departments``— подразделения, в которые группы могут отправлять документы. Представлены структурой ``DepartmentsInGroup`` с полями:

	- ``DepartmentId`` — список идентификаторов подразделений.