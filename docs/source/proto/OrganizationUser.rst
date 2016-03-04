OrganizationUser
================

.. code-block:: protobuf

    message OrganizationUser {
        required string Id = 1;
        required string Name = 2; // ФИО сотрудника
        required OrganizationUserPermissions Permissions = 3;
        required string Position = 4;
    }

    message OrganizationUsersList {
        repeated OrganizationUser Users = 1;
    }    
      

Структура данных *OrganizationUser* содержит информацию о пользователе организации.

-  *Id* - идентификатор пользователя

-  *Name* - ФИО пользователя

-  *Permissions* - права пользователя в организации в виде структуры :doc:`OrganizationUserPermissions`

-  *Position* - должность пользователя

Структура данных *OrganizationUsersList* представляет собой список записей :doc:`OrganizationUser`, возвращаемый методом :doc:`../http/GetOrganizationUsers`.