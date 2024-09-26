EmployeePermissions
===================

На этой странице, помимо ``EmployeePermissions``, описаны следующие структуры и перечисления:

.. contents:: :local:


Структура ``EmployeePermissions`` хранит информацию о правах сотрудника организации.

.. code-block:: protobuf

    message EmployeePermissions {
        required string UserDepartmentId = 1;
        required bool IsAdministrator = 2;
        required DocumentAccessLevel DocumentAccessLevel = 3 [default = UnknownDocumentAccessLevel];
        repeated string SelectedDepartmentIds = 4;
        repeated EmployeeAction Actions = 5;
        optional AuthorizationPermission AuthorizationPermission = 6;
    }

- ``UserDepartmentId`` — идентификатор подразделения организации, в котором состоит сотрудник. Для головного подразделения будет иметь значение ``00000000-0000-0000-0000-000000000000``.
- ``IsAdministrator`` — флаг, означающий, что сотрудник является администратором и может редактировать структуру и реквизиты организации, добавлять и редактировать информацию о других сотрудниках.
- ``DocumentAccessLevel`` — уровень доступа к документам, представленый перечислением :doc:`DocumentAccessLevel`.
- ``SelectedDepartmentIds`` — список подразделений, к которым сотрудник имеет доступ. Заполняется только в случае, если ``DocumentAccessLevel = SelectedDepartments``.
- ``Actions`` — информация о том, на выполнение каких действий сотрудник имеет право. Представлена структурой :ref:`employee_actions`.
- ``AuthorizationPermission`` - информация о наличии ограничения доступа пользователя к сервису, представленная структурой :ref:`authorization-permission`.


.. _employee_actions:

EmployeeAction
--------------

Структура ``EmployeeAction`` содержит информацию о том, может ли сотрудник совершить конкретное действие.

.. code-block:: protobuf

    message EmployeeAction {
        required string Name = 1;
        required bool IsAllowed = 2;
    }

- ``Name`` — строковой идентификатор действия. Принимает одно из следующих значений:

	- ``CreateDocuments`` — создавать и редактировать документы и черновики;
	- ``DeleteRestoreDocuments`` — удалять документы и черновики, восстанавливать документы;
	- ``SignDocuments`` — подписывать документы;
	- ``AddResolutions`` — согласовывать документы;
	- ``RequestResolutions`` — передавать на подпись и согласование;
	- ``ManageCounteragents`` — пидеть списки контрагентов и работать с ними.

- ``IsAllowed`` — флаг, указывающий, разрешено ли сотруднику это действие.


.. _authorization-permission:

AuthorizationPermission
-----------------------

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
	- в структуре :doc:`Employee`
	- в структуре :doc:`EmployeeToCreate`