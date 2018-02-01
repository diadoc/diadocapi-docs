Template
========

Сообщение, содержащее шаблоны документов.

.. code-block:: protobuf

    message Template {
        required string MessageId = 1;
        required sfixed64 TimestampTicks = 2;
        required string FromBoxId = 3;
        required string ToBoxId = 4;
        required string MessageFromBoxId = 5;
        required string MessageToBoxId = 6;
        repeated Entity Entities = 7;
        optional bool IsDeleted = 8 [default = false];
    }

- *MessageId* - уникальный идентификатор сообщения.

- *TimestampTicks* - :doc:`метка времени <Timestamp>` создания сообщения.

- *FromBoxId* - идентификатор ящика отправителя сообщения с шаблонами.

- *ToBoxId* - идентификатор ящика получателя сообщения с шаблонами.

- *MessageFromBoxId* - идентификатор ящика отправителя документов, созданных на основе шаблонов.

- *MessageToBoxId* - идентификатор ящика получателя документов, созданных на основе шаблонов.

- *Entities* - список сущностей, составляющих данное сообщение. Каждая сущность представлена структурой типа :doc:`Entity <Entity message>`.

- *IsDeleted* - флаг, показывающий, было ли удалено данное сообщение.
