UserV2
======

.. code-block:: protobuf

    message UserV2 {
       required string UserId = 1;
       optional string Login = 2;
       optional FullName FullName = 3;
       required bool IsRegistered = 4;
    }

Структура *UserV2* содержит информацию о пользователе. Возвращается методами :doc:`V2/GetMyUser <../http/GetMyUser>`, :doc:`../http/UpdateMyUser`.

- *UserId* - идентификатор пользователя в системе;
- *Login* - логин пользователя;
- *FullName* - фамилия, имя и отчество пользователя, представленные структурой :doc:`FullName`;
- *IsRegistered* - признак того, что пользователь зарегистрирован в системе. Значение false означает, что пользователь был создан в Диадоке с логином, но еще не подтвердил почту.