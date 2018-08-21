SubscriptionsToUpdate
=====================

.. code-block:: protobuf

    message SubscriptionsToUpdate {
        repeated Subscription Subscriptions = 1;
    }

Структура содержит информацию о тех подписках сотрудника на почтовые уведомления, которые необходимо обновить. Принимается методом :doc:`../http/UpdateSubscriptions`.

- :doc:`Subscriptions <Subscription>` - желаемые статусы подписок на конкретные уведомления
