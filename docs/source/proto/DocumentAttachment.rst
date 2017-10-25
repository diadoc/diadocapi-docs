DocumentAttachment
==================

Представляет в отправляемом сообщении :doc:`MessageToPost` документ любого типа.

.. code-block:: protobuf

    message DocumentAttachment {
        required SignedContent SignedContent = 1;
        optional string Comment = 3;
        optional bool NeedRecipientSignature = 4 [default = false];
        repeated DocumentId InitialDocumentIds = 5;
        repeated DocumentId SubordinateDocumentIds = 6;
        optional string CustomDocumentId = 9;
        optional bool NeedReceipt = 10 [default = false];
        repeated CustomDataItem CustomData = 11;
        required string TypeNamedId = 12;
        optional string Function = 13;
        optional string Version = 14;
        repeated MetadataItem Metadata = 15;
        optional int32 WorkflowId = 16;
        optional bool IsEncrypted = 17 [default = false];
    }

-  *SignedContent* - содержимое файла вместе с ЭП под ним в виде структуры :doc:`SignedContent`.

-  *Comment* - необязательный текстовый комментарий к документу.

-  *NeedRecipientSignature* - флаг, обозначающий запрос подписи получателя под отправляемым документом.

-  *InitialDocumentIds* - список идентификаторов документов, к которым привязывается отправляемый документ; каждый такой идентификатор задается структурой :doc:`DocumentId`.

    -  Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку, а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

    -  Если в систему ранее был загружен документ, на него можно сослаться при помощи *InitialDocumentIds*.

    -  В случае отсутствия в системе исходного документа, *InitialDocumentIds* можно не заполнять.

-  *SubordinateDocumentIds* - список идентификаторов документов, которые должны ссылаться на отправляемый документ; каждый такой идентификатор задается структурой :doc:`DocumentId`. Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле DocumentId.MessageId указать пустую строку, а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *CustomDocumentId* - необязательный идентификатор документа во внешней системе, уникальный в рамках структуры :doc:`MessageToPost`; используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через *Document.CustomDocumentId*.

-  *NeedReceipt* - необязательный признак того, что от получателя требуется сформировать извещение о получении данного документа.

-  *CustomData* - список пар вида "ключ-значение", содержащих произвольные данные по документу. Каждая пара задается структурой :doc:`CustomDataItem`.

-  *TypeNamedId* - строковой идентификатор типа документа. Доступные типы можно получить методом :doc:`../http/GetDocumentTypes`.

-  *Function* - идентификатор функции документа. Обязательно при отправке зашифрованных документов.

-  *Version* - идентификатор версии документа. Обязательно при отправке зашифрованных документов.

-  *Metadata* - список пар вида "ключ-значение", содержащих метаданные документа. Каждая пара задается структурой `MetadataItem`_.

-  *WorkflowId* - идентификатор типа документооборота.

-  *IsEncrypted* - флаг, означающий, что документ передается в зашифрованном виде.

MetadataItem
------------

Представляет пару "ключ-значение", привязанную к документу в качестве метаданных.

.. code-block:: protobuf

    message MetadataItem {
        required string Key = 1;
        required string Value = 2;
    }

-  *Key* - непустой ключ. Должен быть валидным ключом метаданных для данного документа.
-  *Value* - непустое значение, соответствующее ключу Key.
