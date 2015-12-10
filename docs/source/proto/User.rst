User
====

.. code-block:: protobuf

    message User {
        optional string Id = 1;
        optional string LastName = 2;
        optional string FirstName = 3;
        optional string MiddleName = 4;
    }
        

Информация о пользователе:

-  *Id* - идентификатор пользователя в системе;

-  *LastName* - фамилия;

-  *FirstName* - имя;

-  *MiddleName* - отчество.