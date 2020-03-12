ContractAttachment
==================

.. code-block:: protobuf

    message ContractAttachment {
        required SignedContent SignedContent = 1;
        required string FileName = 2;
        optional string Comment = 3;
        repeated DocumentId InitialDocumentIds = 4;
        repeated DocumentId SubordinateDocumentIds = 5;
        optional string CustomDocumentId = 6;
        required string DocumentDate = 7;
        required string DocumentNumber = 8;
        optional string ContractPrice = 9;
        optional string ContractType = 10;
        optional bool NeedReceipt = 11 [default = false];
        repeated CustomDataItem CustomData = 12;
    }
        

Структура данных *ContractAttachment* представляет один договор в отправляемом сообщении :doc:`MessageToPost`:

-  *SignedContent* - содержимое файла договора вместе с ЭП под ним в виде структуры :doc:`SignedContent`.

-  *FileName* - имя файла отправляемого договора.

-  *Comment* - необязательный текстовый комментарий к договору.

-  *InitialDocumentIds* - список идентификаторов документов, к которым привязывается отправляемый договор;

    Каждый такой идентификатор задается структурой :doc:`DocumentId`;

    Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку, а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *SubordinateDocumentIds* - список идентификаторов документов, которые должны ссылаться на отправляемый договор;

    Каждый такой идентификатор задается структурой :doc:`DocumentId`;

    Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку, а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *CustomDocumentId* - необязательный идентификатор документа во внешней системе, уникальный в рамках структуры :doc:`MessageToPost`;

    Используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через *Document.CustomDocumentId*.

-  *DocumentDate* - дата составления договора в формате ДД.ММ.ГГГГ.

-  *DocumentNumber* - номер договора.

-  *ContractType* - тип договора (необязательный параметр).

-  *ContractPrice* - цена, указанная в договоре (необязательный параметр).

-  *NeedReceipt* - необязательный признак того, что от получателя требуется сформировать извещение о получении данного документа.

-  *CustomData* - список пар вида "ключ-значение", содержащих произвольные данные по документу. Каждая пара задается структурой :doc:`CustomDataItem`.
