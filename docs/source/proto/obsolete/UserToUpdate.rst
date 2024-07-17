UserToUpdate
============

.. warning::
	Структура используется в устаревшем методе :doc:`../../http/obsolete/UpdateMyUser`.

Структура ``UserToUpdate`` хранит информацию для обновления пользователя.

.. code-block:: protobuf

    message UserToUpdate
    {
        optional UserLoginPatch Login = 1;
        optional UserFullNamePatch FullName = 2;
    }

    message UserLoginPatch
    {
        optional string Login = 1;
    }

    message UserFullNamePatch
    {
        optional FullName FullName = 1;
    }

- ``Login`` — данные для обновления логина пользователя. Если заполнено, то при вызове метода :doc:`../../http/obsolete/UpdateMyUser` будет обновлен логин пользователя. Представлены структурой ``UserLoginPatch`` с полями:

	- ``Login`` — новый логин пользователя. Должен соответствовать формату адреса электронной почты. При выполнения запроса на этот адрес будет отправлено письмо со ссылкой для подтверждения. Не может быть пустым.

- ``FullName`` — данные для обновления ФИО пользователя. Если заполнено, то при вызове метода :doc:`../../http/obsolete/UpdateMyUser` будет обновлены ФИО пользователя.  Представлены структурой ``UserFullNamePatch`` с полями:

	- ``FullName`` — новые фамилия, имя и отчество пользователя, представленные структурой :doc:`../FullName`. Не может быть пустым.

При вызове метода :doc:`../../http/obsolete/UpdateMyUser` в структуре должно быть заполнено хотя бы одно из полей.


----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../../http/obsolete/UpdateMyUser`