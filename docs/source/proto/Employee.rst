Employee
========

Структура ``Employee`` хранит информацию о сотруднике организации.

.. code-block:: protobuf

    message Employee {
       required UserV2 User = 1;
       required EmployeePermissions Permissions = 2;
       required string Position = 3;
       required bool CanBeInvitedForChat = 4;
       optional Timestamp CreationTimestamp = 5;
    }

- ``User`` — информация о пользователе, представленная структурой :doc:`UserV2`.
- ``Permissions`` — информация о правах сотрудника, представленная структурой :doc:`EmployeePermissions`.
- ``Position`` — должность сотрудника/
- ``CanBeInvitedForChat`` — флаг, означающий, что сотрудник отображается в списке получателей сообщений в веб-интерфейсе.
- ``CreationTimestamp`` — дата создания сотрудника, представленная структурой :doc:`Timestamp`.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`EmployeeList`
	- в теле ответа метода :doc:`../http/CreateEmployee`
	- в теле ответа метода :doc:`../http/GetEmployee`
	- в теле ответа метода :doc:`../http/GetMyEmployee`
	- в теле ответа метода :doc:`../http/UpdateEmployee`
	- в устаревшей структуре :doc:`TovTorgBuyerTitleInfo <obsolete/TovTorgInfo>`
	- в устаревшей структуре :doc:`TovTorgTransferInfo <obsolete/TovTorgInfo>`
	- в устаревшей структуре :doc:`TransferInfo <obsolete/UniversalTransferDocumentSellerTitleInfo>`
	- в устаревшей структуре :doc:`obsolete/UniversalTransferDocumentBuyerTitleInfo`