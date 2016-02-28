SupplementaryAgreementAttachment
================================

.. code-block:: protobuf

   message SupplementaryAgreementAttachment {
       required SignedContent SignedContent = 1;
	   required string FileName = 2;
	   optional string Comment = 3;
	   repeated DocumentId InitialDocumentIds = 4;
	   repeated DocumentId SubordinateDocumentIds = 5;
	   optional string CustomDocumentId = 6;
	   required string DocumentDate = 7;
	   required string DocumentNumber = 8;
	   optional string Total = 9;
	   required string ContractNumber = 10;
	   required string ContractDate = 11;
	   optional string ContractType = 12;
	   optional bool NeedReceipt = 13 [default = false];
	   repeated CustomDataItem CustomData = 14;
   }


Структура данных *SupplementaryAgreementAttachment* представляет дополнительное соглашение  к договору в отправляемом сообщении :doc:`MessageToPost`:

-  *SignedContent* - содержимое файла документа вместе с ЭЦП под ним в виде структуры :doc:`SignedContent`.

-  *FileName* - обязательный текстовый комментарий к документу.

-  *Comment* - необязательный текстовый комментарий к документу.

-  *InitialDocumentIds* - список идентификаторов документов, к которым привязывается отправляемый документ; каждый такой идентификатор задается структурой :doc:`DocumentId`.
   
   -  Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку, а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *SubordinateDocumentIds* - список идентификаторов документов, которые должны ссылаться на отправляемый документ; каждый такой идентификатор задается структурой :doc:`DocumentId`.
   
   -  Для того чтобы установить связь с документом внутри отправляемого сообщения, нужно в поле *DocumentId.MessageId* указать пустую строку,а в поле *DocumentId.EntityId* поместить значение поля *CustomDocumentId* соответствующего документа.

-  *CustomDocumentId* - необязательный идентификатор документа во внешней системе, уникальный в рамках структуры :doc:`MessageToPost`; используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через *Document.CustomDocumentId*.

-  *DocumentDate* - дата формирования документа в формате ДД.ММ.ГГГГ.

-  *DocumentNumber* - номер документа.

-  *Total* - цена дополнительного соглашения к договору.

-  *ContractNumber* - номер договора.

-  *ContractDate* - дата договора в формате ДД.ММ.ГГГГ.

-  *ContractType* - тип договора (может отсутствовать).

-  *NeedReceipt* - необязательный признак того, что от получателя требуется сформировать извещение о получении данного документа.

-  *CustomData* - список пар вида "ключ-значение", содержащих произвольные данные по документу. Каждая пара задается структурой :doc:`CustomDataItem <CustomDataItem>`.
