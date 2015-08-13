DocumentId
==========

.. code-block:: protobuf

    message DocumentId
    {
        required string MessageId = 1;
        required string EntityId = 2;
    }

Структура *DocumentId* представляет идентификатор документа:

-  *MessageId* - идентификатор сообщения, содержащего документ.

-  *EntityId* - идентификатор сущности документа внутри сообщения.