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
        optional string EditingSettingId = 18;
    }

-  *SignedContent* - содержимое файла вместе с ЭП под ним в виде структуры :doc:`SignedContent`.

-  *Comment* - необязательный текстовый комментарий к документу. Максимально допустимая длина - 5000 символов.

-  *NeedRecipientSignature* - флаг, обозначающий запрос подписи получателя под отправляемым документом.

-  *InitialDocumentIds* - список идентификаторов документов, к которым привязывается отправляемый документ; каждый такой идентификатор задается структурой :doc:`DocumentId`.

    -  Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку, а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

    -  Если в систему ранее был загружен документ, на него можно сослаться при помощи *InitialDocumentIds*.

    -  В случае отсутствия в системе исходного документа, *InitialDocumentIds* можно не заполнять.

-  *SubordinateDocumentIds* - список идентификаторов документов, которые должны ссылаться на отправляемый документ; каждый такой идентификатор задается структурой :doc:`DocumentId`. Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле DocumentId.MessageId указать пустую строку, а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *CustomDocumentId* - необязательный идентификатор документа во внешней системе, уникальный в рамках структуры :doc:`MessageToPost`; используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через *Document.CustomDocumentId*.

-  *NeedReceipt* - необязательный признак того, что от получателя требуется сформировать извещение о получении данного документа. Для типов, документооборот которых требует безусловную отправку извещения, проставлять в true необязательно.

-  *CustomData* - список пар вида "ключ-значение", содержащих произвольные данные по документу. Каждая пара задается структурой :doc:`CustomDataItem`.

-  *TypeNamedId* - строковой идентификатор типа документа. Доступные типы можно получить методом :doc:`../http/GetDocumentTypes`.

-  *Function* - идентификатор функции документа. Обязательно при отправке зашифрованных документов.

-  *Version* - идентификатор версии документа. Обязательно при отправке зашифрованных документов.

-  *Metadata* - список пар вида "ключ-значение", содержащих метаданные документа. Каждая пара задается структурой :doc:`MetadataItem`. Список доступных метаданных для типа можно получить через метод :doc:`../http/GetDocumentTypes`.

-  *WorkflowId* - идентификатор вида документооборота. Список допустимых видов документооборота для типа можно получить через метод :doc:`../http/GetDocumentTypes`. Описание видов документооборота доступно на странице :doc:`DocumentWorkflow`.

-  *IsEncrypted* - флаг, означающий, что документ передается в зашифрованном виде. Список версий, для которых поддерживается отправка в зашифрованном виде, можно взять из метода :doc:`../http/GetDocumentTypes`.

- *EditingSettingId* - идентификатор настройки редактирования содержимого документа. Наличие данной настройки означает, что в содержимом файла может отсутствовать контент, редактирование которого разрешено данной настройкой.

Примеры использования (C#)
^^^^^^^^^^^^^^^^^^^^^^^^^^

Отправка титула исполнителя для акта о выполнении работ (оказании услуг) в XML-формате:

.. code-block:: csharp

    var attachment = new DocumentAttachment
    {
        TypeNamedId = "XmlAcceptanceCertificate",
        SignedContent = new SignedContent { Content = xmlDocumentBytes, Signature = signatureBytes }
    };

    var messageToPost = new MessageToPost
    {
        FromBoxId = senderBoxId,
        ToBoxId = recepientBoxId,
        DocumentAttachments = { attachment }
    };

    api.PostMessage(token, messageToPost);

Отправка договора с запросом извещения о получении:

.. code-block:: csharp

    var attachment = new DocumentAttachment
    {
        TypeNamedId = "Contract",
        SignedContent = new SignedContent { Content = documentBytes, Signature = signatureBytes },
        Metadata =
        {
            new MetadataItem("FileName", "Договор.pdf"),
            new MetadataItem("DocumentNumber", "196"),
            new MetadataItem("DocumentDate", "27.10.2017"),
            new MetadataItem("ContractType", "Купля-продажа"),
            new MetadataItem("ContractPrice", "3000.00"),
        },
        NeedReceipt = true
    };

    var messageToPost = new MessageToPost
    {
        FromBoxId = senderBoxId,
        ToBoxId = recepientBoxId,
        DocumentAttachments = { attachment }
    };

    api.PostMessage(token, messageToPost);

Отправка зашифрованного счета-фактуры в формате приказа №155:

.. code-block:: csharp

    var attachment = new DocumentAttachment
    {
        TypeNamedId = "Invoice",
        Function = "default",
        Version = "utd_05_01_02",
        SignedContent = new SignedContent
        {
            Content = content,
            Signature = new SignedContent
            {
                Content = encryptedDocumentBytes,
                Signature = signatureBytes
            }
        },
        IsEncrypted = true,
        Metadata =
        {
            new MetadataItem("FileId", "invoice.xml"),
            new MetadataItem("SellerFnsParticipantId", sellerFnsParticipantId),
            new MetadataItem("BuyerFnsParticipantId", buyerFnsParticipantId),
            new MetadataItem("DocumentDate", "27.10.2017"),
            new MetadataItem("DocumentNumber", "169"),
        }
    };

    var messageToPost = new MessageToPost
    {
        FromBoxId = senderBoxId,
        ToBoxId = recepientBoxId,
        DocumentAttachments = { attachment }
    };

    api.PostMessage(token, messageToPost);
