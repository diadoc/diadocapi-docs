UserV2
======

Структура ``UserV2`` хранит информацию о пользователе.

.. code-block:: protobuf

    message UserV2 {
       required string UserId = 1;
       optional string Login = 2;
       optional FullName FullName = 3;
       required bool IsRegistered = 4;
    }

- ``UserId`` — идентификатор пользователя в системе.
- ``Login`` — логин пользователя.
- ``FullName`` — фамилия, имя и отчество пользователя, представленные структурой :doc:`FullName`.
- ``IsRegistered`` — признак того, что пользователь зарегистрирован в системе. Значение ``false`` означает, что пользователь с указанным логином был создан в Диадоке, но еще не подтвердил почту.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :ref:`V2/GetMyUser <GetMyUser_v2>`
	- в теле ответа устаревшего метода :doc:`../http/obsolete/UpdateMyUser`