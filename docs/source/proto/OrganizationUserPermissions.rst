OrganizationUserPermissions
===========================

.. code-block:: protobuf

    message OrganizationUserPermissions {
        required string UserDepartmentId = 1;
        required bool IsAdministrator = 2;
        optional DocumentAccessLevel DocumentAccessLevel = 3 [default = UnknownDocumentAccessLevel];
        required bool CanSignDocuments = 4;
        required bool CanManageCounteragents = 6;
        required bool CanAddResolutions = 7;
        required bool CanRequestResolutions = 8;
        repeated string SelectedDepartmentIds = 9;
        optional string JobTitle = 10;
        required bool CanCreateDocuments = 11;
        required AuthorizationPermission AuthorizationPermission = 12;
        required bool CanDeleteRestoreDocuments = 13;
    }

Структура данных *OrganizationUserPermissions* содержит информацию о правах пользователя в организации.

-  *UserDepartmentId* - идентификатор подразделения организации, в котором состоит пользователь.

    В случае головного подразделения содержит значение 00000000-0000-0000-0000-000000000000.

-  *IsAdministrator* - может ли пользователь редактировать структуру и реквизиты организации, добавлять и редактировать других пользователей.

-  :doc:`DocumentAccessLevel` - уровень доступа к документам

-  *CanSignDocuments* - может ли пользователь подписывать документы.

-  *CanManageCounteragents* - может ли пользователь видеть списки контрагентов и работать с ними.

-  *CanAddResolutions* - может ли пользователь согласовывать документы.

-  *CanRequestResolutions* - может ли пользователь отправлять запросы на согласование и подпись документов.

-  *SelectedDepartmentIds* - список подразделений, к которым имеет доступ пользователь (заполняется только в случае *DocumentAccessLevel = SelectedDepartments*).

-  *JobTitle* - должность пользователя в организации. Может быть не указана.

-  *CanCreateDocuments* - может ли пользователь создавать и редактировать документы и черновики

-  :ref:`AuthorizationPermission <organization-user-authorization-permission>` - данные о наличии ограничения доступа пользователя к сервису

-  *CanDeleteRestoreDocuments* - может ли пользователь удалять документы и черновики, восстанавливать документы

.. _organization-user-authorization-permission:

AuthorizationPermission
-----------------------

.. code-block:: protobuf

    message AuthorizationPermission {
        required bool IsBlocked = 1;
        optional string Comment = 2;
    }

Структура данных *AuthorizationPermission* содержит информацию о наличии ограничений доступа сотрудника к сервису.

    - *IsBlocked* - флаг наличия ограничения доступа пользователя к сервису (``false`` - доступ разрешен, ``true`` - доступ ограничен)

    - *Comment* - причина ограничения доступа пользователя
