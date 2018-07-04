RoamingNotification
===================

.. code-block:: protobuf

    message RoamingNotification
    {
        required Entity Notification = 1;
        required bool IsSuccess = 2;
    }


Структура данных *RoamingNotification* описывает статус доставки документа в роуминг:

-  *IsSuccess* (всегда заполняется) - флаг, обозначающий успешную доставку.

-  :doc:`Notification <Entity>` (может отсутствовать) - описание ошибки доставки.
