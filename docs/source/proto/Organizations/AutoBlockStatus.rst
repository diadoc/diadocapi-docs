AutoBlockStatus
===============

.. code-block:: protobuf

    message AutoBlockStatus
    {
        required bool IsBlocked = 1;
    }

Структура *AutoBlockStatus* содержит информацию о статусе автоматической блокировке ящика на отправку документов.

- *IsBlocked* - заблокирована ли отправка
