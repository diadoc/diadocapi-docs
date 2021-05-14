Docflow API
===========

**Docflow API**   это набор структур данных и HTTP интерфейс для работы в Диадоке. 

С помощью Docflow API можно получать из системы данные о документах и следить за происходящими в ящиках событиями. Этот подход является альтернативой чтению событий через :doc:`http/GetNewEvents`.

Для упрощения работы с API существует SDK (C#/C++/Java/COM), скрывающий детали взаимодействия по HTTP и позволяющий работать с API через набор функций.

HTTP-интерфейс версии 3 
-----------------------

.. toctree::
   :name: toc5
   :maxdepth: 2
   :titlesonly:

   http/GetDocflows_V3
   http/GetDocflowsByPacketId_V3
   http/SearchDocflows_V3
   http/GetDocflowEvents_V3


HTTP-интерфейс (устаревший)
---------------------------

.. toctree::
   :name: toc3
   :maxdepth: 2
   :titlesonly:

   http/GetDocflows
   http/GetDocflowsByPacketId
   http/SearchDocflows
   http/GetDocflowEvents



Структуры данных
----------------

.. toctree::
   :name: toc4
   :maxdepth: 2
   :titlesonly:
   :glob:

   proto/Attachment
   proto/BasicDocumentInfo
   proto/BilateralDocflow
   proto/BuyerTitleDocflow
   proto/CertificateChainElement
   proto/CertificateVerificationResult
   proto/Content
   proto/ContractDocumentInfo
   proto/CustomDataItem
   proto/Docflow
   proto/DocflowV3
   proto/DocflowEvent
   proto/DocflowEventV3
   proto/DocflowStatus
   proto/DocflowStatusV3
   proto/DocflowStatusModel
   proto/DocflowStatusModelV3
   proto/DocflowStatusSeverity
   proto/DocumentDateAndNumber
   proto/DocumentDirection
   proto/DocumentId
   proto/DocumentInfo
   proto/DocumentInfoV3
   proto/DocumentType
   proto/DocumentWithDocflow
   proto/DocumentWithDocflowV3
   proto/Entity
   proto/FetchedDocument
   proto/FetchedDocumentV3
   proto/GetDocflowBatchRequest
   proto/GetDocflowBatchResponse
   proto/GetDocflowBatchResponseV3
   proto/GetDocflowEventsRequest
   proto/GetDocflowEventsResponse
   proto/GetDocflowEventsResponseV3
   proto/GetDocflowRequest
   proto/GetDocflowsByPacketIdRequest
   proto/GetDocflowsByPacketIdResponse
   proto/GetDocflowsByPacketIdResponseV3
   proto/InboundInvoiceDocflow
   proto/InboundInvoiceReceiptDocflow
   proto/InvoiceConfirmationDocflow
   proto/InvoiceCorrectionDocumentInfo
   proto/InvoiceCorrectionRequestDocflow
   proto/InvoiceDocumentInfo
   proto/OutboundInvoiceDocflow
   proto/OuterDocflow
   proto/OuterDocflowEntities
   proto/PriceListDocumentInfo
   proto/ReceiptDocflow
   proto/RecipientSignatureDocflow
   proto/RecipientSignatureRejectionDocflow
   proto/ResolutionDocflowV3
   proto/RevocationDocflow
   proto/RevocationDocflowV3
   proto/ResolutionEntitiesV3
   proto/ResolutionStatusDocflow
   proto/SearchDocflowsRequest
   proto/SearchDocflowsResponse
   proto/SearchScope
   proto/Signature
   proto/SignatureVerificationResult
   proto/SignedAttachment
   proto/SortDirection
   proto/TimeBasedFilter
   proto/Timestamp
   proto/UnilateralDocflow
   proto/utd/docflow/*
   proto/XmlBilateralDocflow
