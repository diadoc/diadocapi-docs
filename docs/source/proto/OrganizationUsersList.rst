OrganizationUsersList
=====================

Структура ``OrganizationUsersList`` представляет собой список пользователей организации.

.. code-block:: protobuf

    message OrganizationUsersList {
        repeated OrganizationUser Users = 1;
    }

    message OrganizationUser {
        required string Id = 1;
        required string Name = 2;
        required OrganizationUserPermissions Permissions = 3;
        required string Position = 4;
    }

- ``Users`` — список пользователей организации, представленных структурой ``OrganizationUser`` с полями:

	- ``Id`` — идентификатор пользователя.
	- ``Name`` — ФИО пользователя.
	- ``Permissions`` — права пользователя в организации, представленные структурой :doc:`OrganizationUserPermissions`.
	- ``Position`` — должность пользователя.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetOrganizationUsers`