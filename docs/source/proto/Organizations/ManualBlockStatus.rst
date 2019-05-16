ManualBlockStatus
=================

.. code-block:: protobuf

    message ManualBlockStatus
    {
        required bool IsBlocked = 1;
        optional sfixed64 RequestedTicks = 2;
    }

Структура *ManualBlockStatus* содержит информацию о ручной блокировке ящика.

- *IsBlocked* - заблокирована ли отправка
- *RequestedTicks* - дата загрузки списка на блокировку
