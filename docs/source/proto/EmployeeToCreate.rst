EmployeeToCreate
================

.. code-block:: protobuf

    message EmployeeToCreate
    {
        required EmployeeToCreateCredentials Credentials = 1;
        optional string Position = 2;
        required bool CanBeInvitedForChat = 3;
        required EmployeePermissions Permissions = 4;
    }

Структура содержит информацию о создаваемом сотруднике организации. Принимается методом :doc:`../http/CreateEmployee`.

- :ref:`Credentials <employee-to-create-credentials>` - реквизиты пользователя, который должен стать сотрудником организации
- *Position* - должность сотрудника
- *CanBeInvitedForChat* - нужно ли отображать сотрудника в списке получателей Сообщений в веб-интерфейсе
- :doc:`Permissions <EmployeePermissions>` - права, которые получит сотрудник

.. _employee-to-create-credentials:

EmployeeToCreateCredentials
---------------------------

.. code-block:: protobuf

    message EmployeeToCreateCredentials
    {
        optional EmployeeToCreateByLogin Login = 1;
        optional EmployeeToCreateByCertificate Certificate = 2;
    }

Структура содержит информацию о реквизитах пользователя, который должен стать сотрудником организации.

- :ref:`Login <employee-to-create-by-login>` - реквизиты в случае, если сотрудник будет работать по электронной почте и паролю
- :ref:`Certificate <employee-to-create-by-certificate>` - реквизиты в случае, если сотрудник будет работать по сертификату КЭП

Должно быть заполнено ровно одно из этих полей.

.. _employee-to-create-by-login:

EmployeeToCreateByLogin
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: protobuf

    message EmployeeToCreateByLogin
    {
        required string Login = 1;
        optional FullName FullName = 2;
    }

Структура содержит информацию о реквизитах пользователя, который будет работать по электронной почте и паролю.

- *Login* - логин пользователя, должен соответствовать формату адреса электронной почты
- :doc:`FullName <UserV2>` - фамилия, имя и отчество создаваемого пользователя. Используется в случае, если пользователя с указанным логином не найдено и создан новый.

.. _employee-to-create-by-certificate:

EmployeeToCreateByCertificate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: protobuf

    message EmployeeToCreateByCertificate
    {
        required bytes Content = 1;
        optional string AccessBasis = 2;
        optional string Email = 3;
    }

Структура содержит информацию о реквизитах пользователя, который будет работать по по сертификату КЭП.

- *Content* - :rfc:`X.509 <5280>` сертификат пользователя, сериализованный в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__.
- *AccessBasis* - основание, на котором пользователь имеет доступ к организации. Требуется заполнить в случае, если ИНН сертификата не совпадает с ИНН организации.
- *Email* - адрес электронной почты сотрудника. В случае, если по сертификату будет создан новый пользователь или найденный пользователь не имеет логина, этот адрес будет установлен в качестве логина, и на него будет отправлено уведомление о добавлении в организацию.
