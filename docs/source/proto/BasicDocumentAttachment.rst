BasicDocumentAttachment
=======================

.. code-block:: protobuf

    message BasicDocumentAttachment {
        required SignedContent SignedContent = 1;
        required string FileName = 2;
        optional string Comment = 3;
        repeated DocumentId InitialDocumentIds = 4;
        repeated DocumentId SubordinateDocumentIds = 5;
        required string DocumentDate = 6;
        required string DocumentNumber = 7;
        required string Total = 8;
        optional string CustomDocumentId = 9;
        optional string Vat = 10;
        optional string Grounds = 11;
        optional bool NeedReceipt = 12 [default = false];
        repeated CustomDataItem CustomData = 13;
    }
        

Структура данных *BasicDocumentAttachment* представляет один первичный бухгалтерский документ (например, счет на оплату, товарную накладную ТОРГ-12, или акт о выполнении работ/оказании услуг) в отправляемом сообщении :doc:`MessageToPost`:

-  *SignedContent* - содержимое файла первичного документа вместе с ЭП под ней в виде структуры :doc:`SignedContent`.

-  *FileName* - имя файла отправляемого первичного документа.

-  *Comment* - необязательный текстовый комментарий к первичному документу.

-  *InitialDocumentIds* - список идентификаторов документов, к которым привязывается отправляемый первичный документ;

    Каждый такой идентификатор задается структурой :doc:`DocumentId`;

    Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку, а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *SubordinateDocumentIds* - список идентификаторов документов, которые должны ссылаться на отправляемый первичный документ;

    Каждый такой идентификатор задается структурой :doc:`DocumentId`;

    Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку, а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *CustomDocumentId* - необязательный идентификатор документа во внешней системе, уникальный в рамках структуры :doc:`MessageToPost`;

    используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через *Document.CustomDocumentId*.

-  *DocumentDate* - дата формирования первичного документа в формате ДД.ММ.ГГГГ.

-  *DocumentNumber* - номер первичного документа.

-  *Total* - сумма первичного документа.

-  *Vat* - сумма НДС первичного документа. Если параметр не заполнен, то первичный документ в Диадоке создается с отметкой "без НДС".

-  *Grounds* - основания для первичного документа, задаются в виде неформализованной строки текста, например, "Договор №1234, Заказ №321".

-  *NeedReceipt* - необязательный признак того, что от получателя требуется сформировать извещение о получении данного документа.

-  *CustomData* - список пар вида "ключ-значение", содержащих произвольные данные по документу. Каждая пара задается структурой :doc:`CustomDataItem`.