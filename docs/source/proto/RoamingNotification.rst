RoamingNotification
===================

.. code-block:: protobuf

    message RoamingNotification
    {
        required Entity Notification = 1;
        required bool Success = 2;
    }
        

Структура данных *RoamingNotification* описывает статус доставки документа в роуминг:

- *Success* - флаг, обозначающий успешную доставку.

- *Notification* - объект типа :doc:`Entity`.
