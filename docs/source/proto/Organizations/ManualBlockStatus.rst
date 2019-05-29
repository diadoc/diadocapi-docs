ManualBlockStatus
=================

.. code-block:: protobuf

    message ManualBlockStatus
    {
        required bool IsBlocked = 1;
        optional sfixed64 RequestedTicks = 2;
    }

Структура *ManualBlockStatus* содержит информацию о ручной блокировке ящика на отправку документов.

- *IsBlocked* - заблокирована ли отправка
- *RequestedTicks* - дата создания задания на блокировку, отправка документов будет заблокирована через 3 дня после создания задания.
