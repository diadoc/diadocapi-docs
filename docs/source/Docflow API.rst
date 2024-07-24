Docflow API
===========

**Docflow API** это набор структур данных и HTTP интерфейс для работы в Диадоке. 

С помощью Docflow API можно получать из системы данные о документах и следить за происходящими в ящиках событиями. Этот подход является альтернативой чтению событий через :doc:`http/GetNewEvents`.

HTTP-интерфейс версии 3 
-----------------------

.. toctree::
   :maxdepth: 2
   :titlesonly:

   http/GetDocflows_V3
   http/GetDocflowsByPacketId_V3
   http/SearchDocflows_V3
   http/GetDocflowEvents_V3

Структуры данных
----------------

.. toctree::
   :maxdepth: 2
   :titlesonly:
   :glob:

   proto/Attachment
   proto/CertificateChainElement
   proto/CertificateVerificationResult
   proto/Content
   proto/CustomDataItem
   proto/DocflowV3
   proto/DocflowEventV3
   proto/DocflowStatusV3
   proto/DocflowStatusModelV3
   proto/DocumentDateAndNumber
   proto/DocumentDirection
   proto/DocumentId
   proto/DocumentInfoV3
   proto/DocumentWithDocflowV3
   proto/Entity
   proto/FetchedDocumentV3
   proto/GetDocflowBatchRequest
   proto/GetDocflowBatchResponseV3
   proto/GetDocflowEventsRequest
   proto/GetDocflowEventsResponseV3
   proto/GetDocflowRequest
   proto/GetDocflowsByPacketIdRequest
   proto/GetDocflowsByPacketIdResponseV3
   proto/OuterDocflow
   proto/OuterDocflowEntities
   proto/ResolutionDocflowV3
   proto/RevocationDocflowV3
   proto/ResolutionEntitiesV3
   proto/ResolutionStatusDocflow
   proto/SearchDocflowsRequest
   proto/SearchDocflowsResponseV3
   proto/SearchScope
   proto/Signature
   proto/SignatureVerificationResult
   proto/SignedAttachment
   proto/SortDirection
   proto/TimeBasedFilter
   proto/Timestamp

Устаревший HTTP-интерфейс
-------------------------

Мы не рекомендуем использовать этот интерфейс в интеграционных решениях.

Методы
~~~~~~

.. toctree::
   :maxdepth: 2
   :titlesonly:

   http/obsolete/GetDocflows_v2
   http/obsolete/GetDocflowsByPacketId_v2
   http/obsolete/SearchDocflows_v2
   http/obsolete/GetDocflowEvents_v2
   
Структуры
~~~~~~~~~

.. toctree::
   :maxdepth: 2
   :titlesonly:

   proto/obsolete/BilateralDocflow
   proto/obsolete/BuyerTitleDocflow
   proto/obsolete/ContractDocumentInfo
   proto/obsolete/Docflow
   proto/obsolete/DocflowEvent
   proto/obsolete/DocumentInfo
   proto/obsolete/DocumentType
   proto/obsolete/DocumentWithDocflow
   proto/obsolete/FetchedDocument
   proto/obsolete/GetDocflowBatchResponse
   proto/obsolete/GetDocflowEventsResponse
   proto/obsolete/GetDocflowsByPacketIdResponse
   proto/obsolete/InboundInvoiceDocflow
   proto/obsolete/InboundInvoiceReceiptDocflow
   proto/obsolete/InvoiceConfirmationDocflow
   proto/obsolete/InvoiceCorrectionDocumentInfo
   proto/obsolete/InvoiceCorrectionRequestDocflow
   proto/obsolete/InvoiceDocumentInfo
   proto/obsolete/OutboundInvoiceDocflow
   proto/obsolete/PriceListDocumentInfo
   proto/obsolete/ReceiptDocflow
   proto/obsolete/RecipientSignatureDocflow
   proto/obsolete/RecipientSignatureRejectionDocflow
   proto/obsolete/RevocationDocflow
   proto/obsolete/SearchDocflowsResponse
   proto/obsolete/UnilateralDocflow
   proto/obsolete/XmlBilateralDocflow