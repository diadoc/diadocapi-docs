DocumentAttachment
==================

Структура ``DocumentAttachment`` представляет собой документ любого типа в отправляемом сообщении :doc:`MessageToPost`.

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

- ``SignedContent`` — содержимое файла вместе с электронной подписью, представленное структурой :doc:`SignedContent`.
- ``Comment`` — текстовый комментарий к документу. Длина не более 5000 символов. Может быть пустым.
- ``NeedRecipientSignature`` — флаг, обозначающий запрос подписи получателя под отправляемым документом.
- ``InitialDocumentIds`` — список идентификаторов документов, к которым привязывается отправляемый документ. Каждый элемент списка представлен структурой :doc:`DocumentId`. Привязка документа работает по следующим правилам:

	- Чтобы установить связь с документом внутри отправляемого сообщения, передайте в поле ``DocumentId.MessageId`` пустую строку, а в поле ``DocumentId.EntityId`` передайте значение поля ``CustomDocumentId`` соответствующего документа.
	- Чтобы установить связь с уже загруженным в систему документом, укажите его идентификатор в поле ``DocumentId.InitialDocumentIds``.

- ``SubordinateDocumentIds`` — список идентификаторов документов, которые должны ссылаться на отправляемый документ. Каждый элемент списка представлен структурой :doc:`DocumentId`. Чтобы установить связь с документом внутри отправляемого сообщения, передайте в поле ``DocumentId.MessageId`` пустую строку, а в поле ``DocumentId.EntityId`` передайте значение поля ``CustomDocumentId`` соответствующего документа.
- ``CustomDocumentId`` — идентификатор документа во внешней системе; используется для выстраивания связей между документами внутри отправляемого сообщения. Должен быть уникальным в рамках структуры :doc:`MessageToPost`. Может быть пустым. После отправки сообщения этот идентификатор можно получить в поле ``CustomDocumentId`` структуры :doc:`Document`. 
- ``NeedReceipt`` — флаг, указывающий, что от получателя требуется сформировать извещение о получении данного документа. Для типов документов, требующих обязательную отправку извещений, указывать необязательно.
- ``CustomData`` — список пользовательских данных (:doc:`тегов <../entities/tag>`), привязанных к документу. Каждый элемент списка представлен структурой :doc:`CustomDataItem`.
- ``TypeNamedId`` — строковой идентификатор типа документа. Доступные типы можно получить методом :doc:`../http/GetDocumentTypes`. Инструкция о получении данных из метода ``GetDocumentTypes`` приведена на странице :doc:`../instructions/getdoctypes`.
- ``Function`` — идентификатор функции документа. Обязателен при отправке зашифрованных документов.
- ``Version`` — идентификатор версии документа. Обязателен при отправке зашифрованных документов.
- ``Metadata`` — список метаданных документа, представленные структурой :doc:`MetadataItem`. Список доступных метаданных для каждого типа документа можно получить с помощью метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных из метода ``GetDocumentTypes`` приведена на странице :doc:`../instructions/getdoctypes`.
- ``WorkflowId`` — идентификатор вида документооборота :doc:`DocumentWorkflow`. Информация о видах документооборота приведена на странице :doc:`../docflows/Workflows`.
- ``IsEncrypted`` — флаг, указывающий, что содержимое передаваемого документа зашифровано. Узнать, поддерживает ли указанная версия документа отправку в зашифрованном виде, можно с помощью метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных из метода ``GetDocumentTypes`` приведена на странице :doc:`../instructions/getdoctypes`.
- ``EditingSettingId`` — идентификатор :doc:`настройки редактирования <../instructions/editingsettings>` содержимого документа.


Примеры использования
---------------------

**Пример заполнения структуры для отправки титула исполнителя для акта о выполнении работ (оказании услуг) в XML-формате (C#):**

.. container:: toggle

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


**Пример заполнения структуры для отправки договора с запросом извещения о получении (C#):**

.. container:: toggle

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


**Пример заполнения структуры для отправки зашифрованного счета-фактуры в формате приказа №155 (C#):**

.. container:: toggle

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


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`MessageToPost`