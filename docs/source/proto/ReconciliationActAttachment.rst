ReconciliationActAttachment
===========================

.. code-block:: protobuf

    message ReconciliationActAttachment {
        required SignedContent SignedContent = 1;
        required string FileName = 2;
        optional string Comment = 3;
        repeated DocumentId InitialDocumentIds = 5;
        repeated DocumentId SubordinateDocumentIds = 6;
        required string DocumentDate = 7;
        required string DocumentNumber = 8;
        optional string CustomDocumentId = 9;
        optional bool NeedReceipt = 10 [default = false];
        repeated CustomDataItem CustomData = 11;
    }
        

Структура данных ReconciliationActAttachment представляет один акт сверки в отправляемом сообщении :doc:`MessageToPost`:

-  SignedContent - содержимое файла ценового листа вместе с ЭЦП под ним в виде структуры :doc:`SignedContent`.

-  FileName - имя файла отправляемого ценового листа.

-  Comment - необязательный текстовый комментарий к ценовому листу.

-  InitialDocumentIds - список идентификаторов документов, к которым привязывается отправляемый ценовой лист; каждый такой идентификатор задается структурой :doc:`DocumentId`. Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле DocumentId.MessageId указать пустую строку, а в поле DocumentId.EntityId поместить значение поля CustomDocumentId соответствующего документа.

-  SubordinateDocumentIds - список идентификаторов документов, которые должны ссылаться на отправляемый ценовой лист; каждый такой идентификатор задается структурой :doc:`DocumentId`. Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле DocumentId.MessageId указать пустую строку, а в поле DocumentId.EntityId поместить значение поля CustomDocumentId соответствующего документа.

-  CustomDocumentId - необязательный идентификатор документа во внешней системе, уникальный в рамках структуры MessageToPost; используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через Document.CustomDocumentId.

-  DocumentDate - дата составления акта сверки в формате ДД.ММ.ГГГГ.

-  DocumentNumber - номер акта сверки.

-  NeedReceipt - необязательный признак того, что от получателя требуется сформировать извещение о получении данного документа.

-  CustomData - список пар вида "ключ-значение", содержащих произвольные данные по документу. Каждая пара задается структурой :doc:`CustomDataItem <CustomDataItem>`.
