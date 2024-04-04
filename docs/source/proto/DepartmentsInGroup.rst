DepartmentsInGroup
==================

Структура ``DepartmentsInGroup`` представляет собой список идентификаторов подразделений, в которые группа контрагентов может отправлять документы.

.. code-block:: protobuf

     message DepartmentsInGroup {
        repeated string DepartmentId = 1;
    }

- ``DepartmentId`` — список идентификаторов подразделений. В списке может быть не больше 419 подразделений.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре ``CounteragentGroupToCreate`` в теле запроса метода :doc:`../http/CreateCounteragentGroup`
	- в структуре ``CounteragentGroupToUpdate`` в теле запроса метода :doc:`../http/UpdateCounteragentGroup`
	- в структуре :doc:`CounteragentGroup`