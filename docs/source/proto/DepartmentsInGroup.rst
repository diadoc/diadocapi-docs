DepartmentsInGroup
==================

Структура ``DepartmentsInGroup`` представляет собой список идентификаторов подразделений, в которые группа контрагентов может отправлять документы.

.. code-block:: protobuf

     message DepartmentsInGroup {
        repeated string DepartmentId = 1;
    }

- ``DepartmentId`` — список идентификаторов подразделений. В списке может быть не больше 419 подразделений.

----

.. rubric:: Смотри также

*Структура используется:*
	- в теле запроса метода :doc:`../http/CreateCounteragentGroup`,
	- в структуре :doc:`CounteragentGroup`, возвращаемой методами

		- :doc:`../http/CreateCounteragentGroup`,
		- :doc:`../http/UpdateCounteragentGroup`.