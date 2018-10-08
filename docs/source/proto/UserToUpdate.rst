UserToUpdate
============

.. code-block:: protobuf

    message UserToUpdate
    {
        optional UserLoginPatch Login = 1;
        optional UserFullNamePatch FullName = 2;
    }

Структура содержит информацию которую необходимо обновить для пользователя. Принимается методом :doc:`../http/UpdateMyUser`.

- :ref:`Login <user-login-patch>` - если поле заполнено, то будет обновлен логин пользователя
- :ref:`FullName <user-full-name-patch>` - если поле заполнено, то будет обновлено ФИО пользователя

Должно быть заполнено хотя-бы одно из этих полей.

.. _user-login-patch:

UserLoginPatch
--------------

.. code-block:: protobuf

    message UserLoginPatch
    {
        optional string Login = 1;
    }

Структура содержит данные для обновления логина пользователя.

- *Login* - новый логин пользователя, должен соответствовать формату адреса электронной почты. При выполнения запроса будет отправлено письмо с ссылкой для подтверждения нового адреса. Поле должно быть заполнено.

.. _user-full-name-patch:

UserFullNamePatch
-----------------

.. code-block:: protobuf

    message UserFullNamePatch
    {
        optional FullName FullName = 1;
    }

Структура содержит данные для обновления ФИО пользователя.

- :doc:`FullName <UserV2>` - новые фамилия, имя и отчество пользователя. Поле должно быть заполнено.