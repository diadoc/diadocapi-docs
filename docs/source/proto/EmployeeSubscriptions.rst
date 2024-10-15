EmployeeSubscriptions
=====================

Структура ``EmployeeSubscriptions`` содержит информацию о подписках сотрудника на почтовые уведомления.

.. code-block:: protobuf

    message EmployeeSubscriptions {
        repeated Subscription Subscriptions = 1;
    }

- ``Subscriptions`` — список статусов подписок на конкретные уведомления, представленных структурой :doc:`Subscription`.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetSubscriptions`
	- в теле ответа метода :doc:`../http/UpdateSubscriptions`