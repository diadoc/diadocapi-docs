EmployeeSubscriptions
=====================

.. code-block:: protobuf

    message EmployeeSubscriptions {
        repeated Subscription Subscriptions = 1;
    }

Структура содержит информацию о подписках сотрудника на почтовые уведомления. Возвращается методами :doc:`../http/GetSubscriptions`, :doc:`../http/UpdateSubscriptions`.

- :doc:`Subscriptions <Subscription>` - статусы подписок на конкретные уведомления
