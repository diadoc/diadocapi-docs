EmployeeToCreate
================

На этой странице, помимо ``EmployeeToCreate``, описаны следующие структуры и перечисления:

.. contents:: :local:


Структура ``EmployeeToCreate`` содержит информацию для создания сотрудника организации.

.. code-block:: protobuf

    message EmployeeToCreate
    {
        required EmployeeToCreateCredentials Credentials = 1;
        optional string Position = 2;
        required bool CanBeInvitedForChat = 3;
        required EmployeePermissions Permissions = 4;
    }

- ``Credentials`` — реквизиты пользователя, представленные структурой :ref:`EmployeeToCreateCredentials`.
- ``Position`` — должность сотрудника.
- ``CanBeInvitedForChat`` — флаг, указывающий, нужно ли отображать сотрудника в списке получателей сообщений в веб-интерфейсе.
- ``Permissions`` — права, которые получит сотрудник, представленные структурой :doc:`EmployeePermissions`.


.. _EmployeeToCreateCredentials:

EmployeeToCreateCredentials
---------------------------

Структура ``EmployeeToCreateCredentials`` содержит информацию о реквизитах пользователя, который должен стать сотрудником организации.

.. code-block:: protobuf

    message EmployeeToCreateCredentials
    {
        optional EmployeeToCreateByLogin Login = 1;
        optional EmployeeToCreateByCertificate Certificate = 2;
    }

- ``Login`` — реквизиты в случае, если сотрудник будет работать по электронной почте и паролю. Представлены структурой :ref:`EmployeeToCreateByLogin`.
- ``Certificate`` — реквизиты в случае, если сотрудник будет работать по сертификату КЭП. Представлены структурой :ref:`EmployeeToCreateByCertificate`.

Должно быть заполнено только одно из этих полей.


.. _EmployeeToCreateByLogin:

EmployeeToCreateByLogin
-----------------------

Структура ``EmployeeToCreateByLogin`` содержит информацию о реквизитах пользователя, который будет работать по электронной почте и паролю.

.. code-block:: protobuf

    message EmployeeToCreateByLogin
    {
        required string Login = 1;
        optional FullName FullName = 2;
    }

- ``Login`` — логин пользователя. Должен соответствовать формату адреса электронной почты.
- ``FullName`` — фамилия, имя и отчество создаваемого пользователя, представленные структурой :doc:`FullName`. Используется для создания нового пользователя в случае, если пользователь с указанным логином не найден.


.. _EmployeeToCreateByCertificate:

EmployeeToCreateByCertificate
-----------------------------

Структура ``EmployeeToCreateByCertificate`` содержит информацию о реквизитах пользователя, который будет работать по по сертификату КЭП.

.. code-block:: protobuf

    message EmployeeToCreateByCertificate
    {
        required bytes Content = 1;
        optional string AccessBasis = 2;
        optional string Email = 3;
    }

- ``Content`` — :rfc:`X.509 <5280>` сертификат пользователя, сериализованный в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__.
- ``AccessBasis`` — основание, на котором пользователь имеет доступ к организации. Нужно заполнить в случае, если ИНН сертификата не совпадает с ИНН организации.
- ``Email`` — адрес электронной почты сотрудника. Будет установлен в качестве логина для найденного пользователя без логина или при создании нового пользователя; на него будет отправлено уведомление о добавлении в организацию.


----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/CreateEmployee`