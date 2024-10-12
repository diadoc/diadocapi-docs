AuthorizationPermission
=======================

Структура ``AuthorizationPermission`` содержит информацию о наличии ограничений доступа сотрудника к сервису.

.. code-block:: protobuf

    message AuthorizationPermission
    {
        required bool IsBlocked = 1;
        optional string Comment = 2;
    }

- ``IsBlocked`` — флаг, указывающий на наличие ограничения доступа пользователя к сервису. Принимает значение:

	- ``false`` — доступ разрешен,
	- ``true`` — доступ ограничен.

- ``Comment`` — причина ограничения доступа пользователя к сервису. Длина не более 500 символов.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`EmployeePermissions`
	- в структуре :doc:`OrganizationUserPermissions`