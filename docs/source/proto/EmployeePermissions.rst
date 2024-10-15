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
- ``SelectedDepartmentIds`` — список идентификаторов подразделений, к которым сотрудник имеет доступ. Заполняется только в случае, если ``DocumentAccessLevel = SelectedDepartments``.
- ``Actions`` — список с информацией о том, на выполнение каких действий сотрудник имеет право. Каждый элемент списка представлен структурой :ref:`EmployeeAction`.
- ``AuthorizationPermission`` - информация о наличии ограничения доступа пользователя к сервису, представленная структурой :doc:`AuthorizationPermission`.


.. _EmployeeAction:

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


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Employee`
	- в структуре :doc:`EmployeeToCreate`