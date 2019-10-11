EmployeePermissions
===================

.. code-block:: protobuf

    message EmployeePermissions {
        required string UserDepartmentId = 1;
        required bool IsAdministrator = 2;
        required DocumentAccessLevel DocumentAccessLevel = 3 [default = UnknownDocumentAccessLevel];
        repeated string SelectedDepartmentIds = 4;
        repeated EmployeeAction Actions = 5;
        optional AuthorizationPermission AuthorizationPermission = 6;
    }

Структура *EmployeePermissions* содержит информацию о правах сотрудника организации. Как часть структуры :doc:`Employee` возвращается методами :doc:`../http/GetEmployee`, :doc:`../http/CreateEmployee`, :doc:`../http/UpdateEmployee`.

- *UserDepartmentId* - идентификатор подразделения организации, в котором состоит сотрудник. В случае головного подразделения содержит значение 00000000-0000-0000-0000-000000000000
- *IsAdministrator* - может ли сотрудник редактировать структуру и реквизиты организации, добавлять и редактировать других сотрудников
- :doc:`DocumentAccessLevel` - уровень доступа к документам
- *SelectedDepartmentIds* - список подразделений, к которым имеет доступ сотрудник (заполняется только в случае *DocumentAccessLevel = SelectedDepartments*).
- :ref:`Actions <actions>` - информация о том, какие действия имеет право выполнять сотрудник
- :ref:`AuthorizationPermission <authorization-permission>` - информация о наличии ограничения доступа пользователя к сервису

.. _actions:

EmployeeAction
--------------

.. code-block:: protobuf

    message EmployeeAction {
        required string Name = 1;
        required bool IsAllowed = 2;
    }

Структура *EmployeeAction* содержит информацию о том, может ли сотрудник совершить конкретное действие.

- *Name* - строковой идентификатор действия
- *IsAllowed* - разрешено ли действие

.. csv-table:: Действия сотрудников
   :header: "Идентификатор", "Описание"
   :widths: 2, 10

   "CreateDocuments", "Создавать и редактировать документы и черновики"
   "DeleteRestoreDocuments", "Удалять документы и черновики, восстанавливать документы"
   "SignDocuments", "Подписывать документы"
   "AddResolutions", "Согласовывать документы"
   "RequestResolutions", "Передавать на подпись и согласование"
   "ManageCounteragents", "Видеть списки контрагентов и работать с ними"

.. _authorization-permission:

AuthorizationPermission
-----------------------

.. code-block:: protobuf

    message AuthorizationPermission
    {
        required bool IsBlocked = 1;
        optional string Comment = 2;
    }

Структура *AuthorizationPermission* содержит информацию о наличии ограничений доступа сотрудника к сервису.

- *IsBlocked* - флаг наличия ограничения доступа пользователя к сервису (``false`` - доступ разрешен, ``true`` - доступ ограничен)

- *Comment* - причина ограничения доступа пользователя к сервису
