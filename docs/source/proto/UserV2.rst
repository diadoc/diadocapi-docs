UserV2
======

.. code-block:: protobuf

    message UserV2 {
       required string UserId = 1;
       optional string Login = 2;
       optional FullName FullName = 3;
       required bool IsRegistered = 4;
    }

    message FullName {
        required string LastName = 1;
        required string FirstName = 2;
        optional string MiddleName = 3;
    }

Структура *UserV2* содержит информацию о пользователе. Возвращается методами :doc:`V2/GetMyUser <../http/GetMyUser>`, :doc:`../http/UpdateMyUser`.

- *UserId* - идентификатор пользователя в системе;
- *Login* - логин пользователя;
- *FullName* - фамилия, имя и отчество пользователя;
- *IsRegistered* - признак того, что пользователь зарегистрирован в системе. Значение false означает, что пользователь был создан в Диадоке с логином, но еще не подтвердил почту.

Структура *FullName* содержит фамилию, имя и отчество пользователя.

- *LastName* - фамилия;
- *FirstName* - имя;
- *MiddleName* - отчество.