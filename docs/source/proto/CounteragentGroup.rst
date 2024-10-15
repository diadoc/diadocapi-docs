CounteragentGroup
=================

Структура ``CounteragentGroup`` хранит информацию о группе контрагентов.

.. code-block:: protobuf

    message CounteragentGroup {
        required string CounteragentGroupId = 1;
        required string Name = 2;
        optional DepartmentsInGroup Departments = 3;
    }

- ``CounteragentGroupId`` — идентификатор группы контрагентов.
- ``Name`` — название группы контрагентов.
- ``Departments``— список подразделений, в которые группы могут отправлять документы. Представлен структурой :doc:`DepartmentsInGroup`. Если отстутствует, контрагенты группы могут отправлять документы в любое подразделение.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре ``CounteragentGroupsList``, возвращаемой методом :doc:`../http/GetCounteragentGroups`
	- в теле ответа метода :doc:`../http/CreateCounteragentGroup`
	- в теле ответа метода :doc:`../http/GetCounteragentGroup`
	- в теле ответа метода :doc:`../http/UpdateCounteragentGroup`

*Определение:*
	- :doc:`../entities/counteragent`

*Инструкции:*
	- :doc:`../instructions/counteragentgroups`