RoamingNotification
===================

.. code-block:: protobuf

    message RoamingNotification
    {
        required bool Success = 1;
        optional string Description = 2;
    }
        

Структура данных *RoamingNotification* описывает статус доставки документа в роуминг:

-  *Success* (всегда заполняется) - флаг, обозначающий успешную доставку.

-  *Description* (может отсутствовать) - описание ошибки доставки.
