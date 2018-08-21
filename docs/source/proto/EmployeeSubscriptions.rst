EmployeeSubscriptions
=====================

.. code-block:: protobuf

    message EmployeeSubscriptions {
        repeated Subscription Subscriptions = 1;
    }

Структура содержит информацию о подписках сотрудника на почтовые уведомления. Возвращается методом :doc:`../http/GetSubscriptions`.

- :doc:`Subscriptions <Subscription>` - статусы подписок на конкретные уведомления
