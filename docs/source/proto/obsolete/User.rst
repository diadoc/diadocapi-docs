User
====

.. warning::
	Структура устарела. Вместо нее используется структура :doc:`../UserV2`.

Структура ``User`` хранит информацию о пользователе.

.. code-block:: protobuf

    message User {
        optional string Id = 1;
        optional string LastName = 2;
        optional string FirstName = 3;
        optional string MiddleName = 4;
    }

- ``Id`` - идентификатор пользователя в системе.
- ``LastName`` - Фамилия пользователя.
- ``FirstName`` - имя пользователя.
- ``MiddleName`` - отчество пользователя.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа устаревшего метода :ref:`GetMyUser <GetMyUser_v1>`