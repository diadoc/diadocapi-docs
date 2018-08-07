PacketInfo
==========

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message PacketInfo
    {
       required LockMode LockMode = 1;
       optional string PacketId = 2; // актуально только для письма
       optional Timestamp AddedAt = 3; // актуально только для письма
    }

Структура содержит информацию о связанных документах.

- :doc:`LockMode` - режим блокировки пакета
- *PacketId* - идентификатор пакета, в котором в данный момент находится документ
- :doc:`AddedAt <Timestamp>` - метка времени добавления документа в пакет
