BlockStatus
===========

.. code-block:: protobuf

    message BlockStatus
    {
        required ManualBlockStatus ManualBlockStatus = 1;
        required AutoBlockStatus AutoBlockStatus = 2;
    }

Структура *BlockStatus* содержит информацию о статусе блокировки ящика на отправку документов.

- :doc:`ManualBlockStatus <ManualBlockStatus>` - статус ручной блокировки отправки
- :doc:`AutoBlockStatus <AutoBlockStatus>` - статус автоматической блокировки отправки  
