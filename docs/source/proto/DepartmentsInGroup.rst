DepartmentsInGroup
==================

Структура ``DepartmentsInGroup`` хранит список идентификаторов подразделений, в которые группа контрагентов может отправлять документы.

.. code-block:: protobuf

     message DepartmentsInGroup {
        repeated string DepartmentId = 1;
    }

- ``DepartmentId`` — список идентификаторов подразделений. В списке может быть не больше 419 подразделений.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`CounteragentGroup`
	- в структуре ``CounteragentGroupToCreate`` в теле запроса метода :doc:`../http/CreateCounteragentGroup`
	- в структуре ``CounteragentGroupToUpdate`` в теле запроса метода :doc:`../http/UpdateCounteragentGroup`

*Определение:*
	- :doc:`../entities/counteragent`

*Инструкции:*
	- :doc:`../instructions/counteragentgroups`