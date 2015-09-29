EncryptedInvoiceAttachment
==========================

.. code-block:: protobuf

    message EncryptedInvoiceAttachment {
	    required SignedContent SignedContent = 1;
	    optional string Comment = 3;
	    repeated DocumentId InitialDocumentIds = 4;
	    repeated DocumentId SubordinateDocumentIds = 5;
	    optional string CustomDocumentId = 6;
	    repeated CustomDataItem CustomData = 7;
	    required EncryptedDocumentMetadata Metadata = 8;
	    optional EncryptedInvoiceMetadata InvoiceMetadata = 9;
	    optional EncryptedInvoiceCorrectionMetadata InvoiceCorrectionMetadata = 10;
    }

    message EncryptedInvoiceMetadata {
	    optional DocumentDateAndNumber RevisionDateAndNumber = 1;
    }

    message EncryptedInvoiceCorrectionMetadata {
	    required DocumentDateAndNumber OriginalInvoiceDateAndNumber = 1;
	    optional DocumentDateAndNumber OriginalInvoiceRevisionDateAndNumber = 2;
	    optional DocumentDateAndNumber InvoiceCorrectionRevisionDateAndNumber = 3;
    }

        
Структура данных *EncryptedInvoiceAttachment* представляет зашифрованный счет-фактуру в отправляемом сообщении :doc:`MessageToPost`:

-  *SignedContent* - содержимое файла документа вместе с ЭЦП под ним в виде структуры :doc:`SignedContent`.

-  *Comment* - необязательный текстовый комментарий к документу.

-  *InitialDocumentIds* - список идентификаторов документов, к которым привязывается отправляемый документ; каждый такой идентификатор задается структурой :doc:`DocumentId`.
   
   -  Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку, а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *SubordinateDocumentIds* - список идентификаторов документов, которые должны ссылаться на отправляемый документ; каждый такой идентификатор задается структурой :doc:`DocumentId`.
   
   -  Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку,а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *CustomDocumentId* - необязательный идентификатор документа во внешней системе, уникальный в рамках структуры :doc:`MessageToPost`; используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через *Document.CustomDocumentId*.

-  *CustomData* - список пар вида "ключ-значение", содержащих произвольные данные по документу. Каждая пара задается структурой :doc:`CustomDataItem <CustomDataItem>`.
   
-  *Metadata* - метаданные зашифрованного документа в отправляемом сообщении :doc:`MessageToPost`, представленные структурой :doc:`EncryptedDocumentMetadata`.
   
-  *InvoiceMetadata* - метаданные исправления зашифрованного счета-фактуры в отправляемом сообщении :doc:`MessageToPost`, представленные структурой *EncryptedInvoiceMetadata*. Заполняется в случае, если передается исправление счет-фактуры (ИСФ) и содержит номер и дату исправления.
   
-  *InvoiceCorrectionMetadata* - метаданные корректировки зашифрованного счета-фактуры (корректировки исправления счета-фактуры) в отправляемом сообщении :doc:`MessageToPost`, представленные структурой *InvoiceCorrectionMetadata*

Структура *EncryptedInvoiceMetadata* представляет метаданные исправления зашифрованного счета-фактуры в отправляемом сообщении :doc:`MessageToPost`:

-  *DocumentDateAndNumber* - дата и номер исправления счета-фактуры, представленные в виде структуры :doc:`DocumentDateAndNumber`.

Структура *EncryptedInvoiceCorrectionMetadata* представляет метаданные корректировки зашифрованного счета-фактуры (корректировки исправления счета-фактуры) в отправляемом сообщении :doc:`MessageToPost`:

-  *OriginalInvoiceDateAndNumber* - дата и номер счета-фактуры, к которому выставляется корректировка, представленные в виде структуры :doc:`DocumentDateAndNumber`.

-  *OriginalInvoiceRevisionDateAndNumber* - дата и номер исправления счета-фактуры, к которому выставляется корректировка, представленные в виде структуры :doc:`DocumentDateAndNumber`.

-  *InvoiceCorrectionRevisionDateAndNumber* - дата и номер корректировки счета-фактуры, представленные в виде структуры :doc:`DocumentDateAndNumber`.
