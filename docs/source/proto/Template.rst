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
        optional string MessageToDepartmentId = 9;
        required LockMode LockMode = 10;
        optional string MessageProxyBoxId = 11;
        optional string MessageProxyDepartmentId = 12; 
        optional bool IsReusable = 13 [default = false];
    }

- *MessageId* - уникальный идентификатор сообщения с шаблонами.

- *TimestampTicks* - :doc:`метка времени <Timestamp>` создания сообщения.

- *FromBoxId* - идентификатор ящика отправителя сообщения с шаблонами.

- *ToBoxId* - идентификатор ящика получателя сообщения с шаблонами.

- *MessageFromBoxId* - идентификатор ящика отправителя документов, созданных на основе шаблонов.

- *MessageToBoxId* - идентификатор ящика получателя документов, созданных на основе шаблонов.

- *Entities* - список сущностей, составляющих данное сообщение. Каждая сущность представлена структурой типа :doc:`Entity <Entity message>`.

- *IsDeleted* - флаг, показывающий, было ли удалено данное сообщение.

- *MessageToDepartmentId* - идентификатор подразделения получателя сообщения, которое будет создано на основе шаблона.

- *LockMode* - режим блокировки сообщения с шаблонами. Виды доступных режимы доступны в описании :doc:`../proto/LockMode`.

- *MessageProxyBoxId* - идентификатор ящика промежуточного получателя документов, созданных на основе шаблонов.

- *MessageProxyDepartmentId* - идентификатор подразделения промежуточного получателя сообщения, которое будет создано на основе отправляемого шаблона.

- *IsReusable* - флаг, показывающий, является ли шаблон многоразовым.