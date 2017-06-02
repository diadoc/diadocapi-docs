EncryptedXmlDocumentAttachment
==============================

.. code-block:: protobuf

   message EncryptedXmlDocumentAttachment {
       required SignedContent SignedContent = 1;
       optional string Comment = 3;
       repeated DocumentId InitialDocumentIds = 4;
       repeated DocumentId SubordinateDocumentIds = 5;
       optional string CustomDocumentId = 6;
       repeated CustomDataItem CustomData = 7;
       required EncryptedDocumentMetadata Metadata = 8;
       required EncryptedXmlBasicDocumentMetadata XmlBasicMetadata = 9;
   }
   
   message EncryptedXmlBasicDocumentMetadata {
       required string FormationDate = 1;
       required string FormationTime = 2;
       optional string DocumentName = 3;
   }



Структура данных *EncryptedXmlDocumentAttachment* представляет зашифрованный формализованный документ (накладную ТОРГ-12 или акт) в отправляемом сообщении :doc:`MessageToPost`:

-  *SignedContent* - содержимое файла документа вместе с ЭП под ним в виде структуры :doc:`SignedContent`.

-  *Comment* - необязательный текстовый комментарий к документу.

-  *InitialDocumentIds* - список идентификаторов документов, к которым привязывается отправляемый документ; каждый такой идентификатор задается структурой :doc:`DocumentId`.
   
   -  Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку, а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *SubordinateDocumentIds* - список идентификаторов документов, которые должны ссылаться на отправляемый документ; каждый такой идентификатор задается структурой :doc:`DocumentId`.
   
   -  Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку,а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *CustomDocumentId* - необязательный идентификатор документа во внешней системе, уникальный в рамках структуры :doc:`MessageToPost`; используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через *Document.CustomDocumentId*.

-  *CustomData* - список пар вида "ключ-значение", содержащих произвольные данные по документу. Каждая пара задается структурой :doc:`CustomDataItem <CustomDataItem>`.
   
-  *Metadata* - метаданные зашифрованного документа в отправляемом сообщении :doc:`MessageToPost`, представленные структурой :doc:`EncryptedDocumentMetadata`.

-  *XmlBasicMetadata* - метаданные, специфичные для формализованных ТОРГ-12 и актов, представленные структурой *EncryptedXmlBasicDocumentMetadata*.

Структура *EncryptedXmlBasicDocumentMetadata* представляет метаданные формализованных ТОРГ-12 и актов в отправляемом сообщении :doc:`MessageToPost`:

-  *FormationDate* - дата формирования зашифрованного XML-документа. Значение должно совпадать со значением атрибута ДатаДок в теге Документ в зашифрованном контенте.

-  *FormationTime* - время формирования зашифрованного XML-документа. Значение должно совпадать со значением атрибута ВремДок в теге Документ в зашифрованном контенте.

-  *DocumentName* - наименование первичного документа, определенное организацией (НаимДокОпр)