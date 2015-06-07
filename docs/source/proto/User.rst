User
====

.. code-block:: protobuf

    message User {
        optional string Id = 1;
        optional string LastName = 2;
        optional string FirstName = 3;
        optional string MiddleName = 4;
    }
        

Информация о пользователе.

-  *Id* - Идентификатор пользователя в системе;

-  *LastName* - Фамилия;

-  *FirstName* - Имя;

-  *MiddleName* - Отчество;