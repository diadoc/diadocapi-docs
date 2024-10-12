EmployeeToUpdate
================

На этой странице, помимо ``EmployeeToCreate``, описаны следующие структуры и перечисления:

.. contents:: :local:


Структура ``EmployeeToUpdate`` содержит информацию для изменения данных сотрудника.

.. code-block:: protobuf

    message EmployeeToUpdate
    {
        optional EmployeePermissionsPatch Permissions = 1;
        optional EmployeePositionPatch Position = 2;
        optional EmployeeCanBeInvitedForChatPatch CanBeInvitedForChat = 3;
    }

- ``Permissions`` — информация о разрешениях сотрудника, представленные структурой :ref:`EmployeePermissionsPatch`.
- ``Position`` — информация о должности сотрудника, представленная структурой :ref:`EmployeePositionPatch`.
- ``CanBeInvitedForChat`` — информация о необходимости отображать сотрудника в списке получателей сообщений в веб-интерфейсе, представленная структурой :ref:`EmployeeCanBeInvitedForChatPatch`.

Нужно заполнить только те данные, которые требуется изменить.


.. _EmployeePermissionsPatch:

EmployeePermissionsPatch
------------------------

Структура ``EmployeePermissionsPatch`` содержит информацию для изменения :doc:`разрешений сотрудника <EmployeePermissions>`.

.. code-block:: protobuf

    message EmployeePermissionsPatch
    {
        optional EmployeeDepartmentPatch Department = 1;
        optional EmployeeIsAdministratorPatch IsAdministrator = 2;
        optional EmployeeDocumentAccessLevelPatch DocumentAccessLevel = 3;
        optional EmployeeSelectedDepartmentsPatch SelectedDepartments = 4;
        repeated EmployeeAction Actions = 5;
        optional AuthorizationPermissionPatch AuthorizationPermission = 6;
    }

- ``Department`` — информация о подразделении сотрудника, представленная структурой :ref:`EmployeeDepartmentPatch`.
- ``IsAdministrator`` — информация о праве сотрудника администрировать организацию, представленная стркутурой :ref:`EmployeeIsAdministratorPatch`.
- ``DocumentAccessLevel`` — информация об уровне доступа сотрудника к документам, представленная структрой :ref:`EmployeeDocumentAccessLevelPatch`.
- ``SelectedDepartments`` — информация о подразделениях, к которым сотрудник имеет доступ, представленная структурой :ref:`EmployeeSelectedDepartmentsPatch`. Имеет смысл только в случае, если ``DocumentAccessLevel = SelectedDepartments``.
- ``Actions`` — информация о действиях сотрудника, права на которые нужно добавить или убрать, представленная структурой :doc:`EmployeePermissions`.
- ``AuthorizationPermission`` — информация об ограничениях доступа сотрудника к сервису, представленная структурой :ref:`AuthorizationPermissionPatch`.

Нужно заполнить только те данные, которые требуется изменить.


.. _EmployeePositionPatch:

EmployeePositionPatch
---------------------

Структура ``EmployeePositionPatch`` содержит информацию для изменения должности сотрудника.

.. code-block:: protobuf

    message EmployeePositionPatch
    {
        optional string Position = 1;
    }

- ``Position`` — должность сотрудника.


.. _EmployeeCanBeInvitedForChatPatch:

EmployeeCanBeInvitedForChatPatch
--------------------------------

Структура ``EmployeeCanBeInvitedForChatPatch`` содержит информацию для изменения необходимости отображать сотрудника в списке получателей cообщений в веб-интерфейсе.

.. code-block:: protobuf

    message EmployeeCanBeInvitedForChatPatch
    {
        required bool CanBeInvitedForChat = 1;
    }

- ``CanBeInvitedForChat`` — флаг, указывающий, нужно ли отображать сотрудника в списке получателей сообщений в веб-интерфейсе.


.. _EmployeeDepartmentPatch:

EmployeeDepartmentPatch
-----------------------

Структура ``EmployeeDepartmentPatch`` содержит информацию для изменения подразделения сотрудника.

.. code-block:: protobuf

    message EmployeeDepartmentPatch
    {
        required string DepartmentId = 1;
    }

- ``DepartmentId`` — идентификатор подразделения, в которое нужно переместить сотрудника.


.. _EmployeeIsAdministratorPatch:

EmployeeIsAdministratorPatch
----------------------------

Структура ``EmployeeIsAdministratorPatch`` содержит информацию для изменения права сотрудника администрировать организацию.

.. code-block:: protobuf

    message EmployeeDepartmentPatch
    {
        required bool IsAdministrator = 1;
    }

- ``IsAdministrator`` — флаг, указывающий, имеет ли сотрудник право администрировать организацию.


.. _EmployeeDocumentAccessLevelPatch:

EmployeeDocumentAccessLevelPatch
--------------------------------

Структура ``EmployeeDocumentAccessLevelPatch`` содержит информацию для изменения уровня доступа сотрудника к документам.

.. code-block:: protobuf

    message EmployeeDocumentAccessLevelPatch
    {
        required DocumentAccessLevel DocumentAccessLevel = 1;
    }

- ``DocumentAccessLevel`` — уровень доступа сотрудника к документам, представленный структурой :doc:`DocumentAccessLevel`.


.. _EmployeeSelectedDepartmentsPatch:

EmployeeSelectedDepartmentsPatch
--------------------------------

Структура ``EmployeeSelectedDepartmentsPatch`` содержит информацию для изменения списка подразделений, к которым сотрудник имеет доступ.

.. code-block:: protobuf

    message EmployeeSelectedDepartmentsPatch
    {
        repeated string SelectedDepartmentIds = 1;
    }

- ``SelectedDepartmentIds`` — список подразделений, к которым имеет доступ сотрудник.


.. _AuthorizationPermissionPatch:

AuthorizationPermissionPatch
----------------------------

Структура ``AuthorizationPermissionPatch`` содержит информацию для изменения данных об ограничениях доступа сотрудника к сервису.

.. code-block:: protobuf

    message AuthorizationPermissionPatch
    {
        required bool IsBlocked = 1;
        optional string Comment = 2;
    }

- ``IsBlocked`` — флаг, указывающий на наличие ограничения доступа сотрудника к сервису. Принимает значения:

	- ``true`` — доступ ограничен,
	- ``false`` — доступ разрешен.

- ``Comment`` — причина ограничения доступа сотрудника к сервису. Длина не более 500 символов.



----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/UpdateEmployee`