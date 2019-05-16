BlockStatus
===========

.. code-block:: protobuf

    message BlockStatus
    {
        required ManualBlockStatus ManualBlockStatus = 1;
        required AutoBlockStatus AutoBlockStatus = 2;
    }

Структура *BlockStatus* содержит информацию о статусе блокировки и BoxFeatures ящика.

- :doc:`ManualBlockStatus <ManualBlockStatus>` - статус ручной блокировки организации
- :doc:`AutoBlockStatus <AutoBlockStatus>` - статус автоблокировки организации (на основании текущего пакета)