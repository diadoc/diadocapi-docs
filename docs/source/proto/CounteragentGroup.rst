CounteragentGroup
=================

Структура ``CounteragentGroup`` представляет собой группу контрагентов.

.. code-block:: protobuf

    message CounteragentGroup {
        required string CounteragentGroupId = 1;
        required string Name = 2;
        optional DepartmentsInGroup Departments = 3;
    }

- ``CounteragentGroupId`` — идентификатор группы контрагентов.
- ``Name`` — название группы контрагентов.
- ``Departments``— список подразделений, в которые группы могут отправлять документы. Представлен структурой :doc:`DepartmentsInGroup`.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`Counteragent`,
	- в структуре :doc:`GetOrganizationsByInnListResponse`,
	- в теле ответа метода :doc:`../http/CreateCounteragentGroup`,
	- в теле ответа метода :doc:`../http/UpdateCounteragentGroup`,