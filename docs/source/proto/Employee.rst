Employee
========

.. code-block:: protobuf

    message Employee {
       required UserV2 User = 1;
       required EmployeePermissions Permissions = 2;
       required string Position = 3;
       required bool CanBeInvitedForChat = 4;
       optional Timestamp CreationTimestamp = 5;
    }

Структура содержит информацию о сотруднике организации. Возвращается методами :doc:`../http/GetEmployee`, :doc:`../http/CreateEmployee`, :doc:`../http/UpdateEmployee`, :doc:`../http/GetMyEmployee`.

 - :doc:`User <UserV2>` - информация о пользователе
 - :doc:`Permissions <EmployeePermissions>` - права сотрудника
 - *Position* - должность сотрудника
 - *CanBeInvitedForChat* - сотрудник отображается в списке получателей Сообщений в веб-интерфейсе
 - :doc:`CreationTimestamp <Timestamp>` - дата создания сотрудника
