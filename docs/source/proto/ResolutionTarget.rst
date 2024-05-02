ResolutionTarget
================

Структура ``ResolutionTarget`` содержит информацию о том, кому направлен запрос на согласование.

.. code-block:: protobuf

    message ResolutionTarget {
        optional string Department = 1;
        optional string DepartmentId = 2;
        optional string User = 3;
        optional string UserId = 4;
    }

- ``Department`` — название подразделения, в которое направлен запрос.
- ``DepartmentId`` — идентификатор подразделения, в которое направлен запрос.
- ``User`` — ФИО пользователя, которому направлен запрос.
- ``UserId`` — идентификатор пользователя, которому направлен запрос.

Если запрос отправлен конкретному сотруднику, то будут заполены свойства ``User`` и ``UserId``, если в подразделение — ``Department`` и ``DepartmentId``.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`ResolutionRequestInfo`
	- в структуре :ref:`ResolutionRequestV3`