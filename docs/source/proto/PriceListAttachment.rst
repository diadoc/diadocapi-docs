PriceListAttachment
===================

.. code-block:: protobuf

    message PriceListAttachment {
        required SignedContent SignedContent = 1;
        required string FileName = 2;
        optional string Comment = 3;
        repeated DocumentId InitialDocumentIds = 4;
        repeated DocumentId SubordinateDocumentIds = 5;
        optional string CustomDocumentId = 6;
        required string DocumentDate = 7;
        required string DocumentNumber = 8;
        required string PriceListEffectiveDate = 9;
        required string ContractDocumentDate = 10;
        required string ContractDocumentNumber = 11;
        optional bool NeedReceipt = 12 [default = false];
        repeated CustomDataItem CustomData = 13;
    }
        

Структура данных PriceListAttachment представляет один ценовой лист в отправляемом сообщении :doc:`MessageToPost`:

-  SignedContent - содержимое файла ценового листа вместе с ЭЦП под ним в виде структуры :doc:`SignedContent`.

-  FileName - имя файла отправляемого ценового листа.

-  Comment - необязательный текстовый комментарий к ценовому листу.

-  InitialDocumentIds - список идентификаторов документов, к которым привязывается отправляемый ценовой лист; каждый такой идентификатор задается структурой :doc:`DocumentId`. Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле DocumentId.MessageId указать пустую строку, а в поле DocumentId.EntityId поместить значение поля CustomDocumentId соответствующего документа.

-  SubordinateDocumentIds - список идентификаторов документов, которые должны ссылаться на отправляемый ценовой лист; каждый такой идентификатор задается структурой :doc:`DocumentId`. Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле DocumentId.MessageId указать пустую строку, а в поле DocumentId.EntityId поместить значение поля CustomDocumentId соответствующего документа.

-  CustomDocumentId - необязательный идентификатор документа во внешней системе, уникальный в рамках структуры MessageToPost; используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через Document.CustomDocumentId.

-  DocumentDate - дата составления ценового листа в формате ДД.ММ.ГГГГ.

-  DocumentNumber - номер ценового листа.

-  PriceListEffectiveDate - дата вступления в силу ценового листа в формате ДД.ММ.ГГГГ.

-  ContractDocumentDate - дата составления договора, к которому относится ценовой лист в формате ДД.ММ.ГГГГ.

-  ContractDocumentNumber - номер договора, к которому относится ценовой лист.

-  NeedReceipt - необязательный признак того, что от получателя требуется сформировать извещение о получении данного документа.

-  CustomData - список пар вида "ключ-значение", содержащих произвольные данные по документу. Каждая пара задается структурой
   :doc:`CustomDataItem <CustomDataItem>`.