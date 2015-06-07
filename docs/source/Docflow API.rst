Docflow API
===========

**Docflow API**   это набор структур данных и HTTP интерфейс для работы в Диадоке. 

С помощью Docflow API можно получать из системы данные о документах и следить за происходящими в ящиках событиями (для отправки документов и работы с организациями можно оспользоваться `старой версией API <https://diadoc.kontur.ru/sdk/>`_).

Для упрощения работы с API существует SDK (C#/C++/Java/COM), скрывающий детали взаимодействия по HTTP и позволяющий работать с API через набор функций.

HTTP-интерфейс
--------------

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
   proto/DocflowEvent
   proto/DocflowStatus
   proto/DocflowStatusModel
   proto/DocflowStatusSeverity
   proto/DocumentDateAndNumber
   proto/DocumentDirection
   proto/DocumentId
   proto/DocumentInfo
   proto/DocumentType
   proto/DocumentWithDocflow
   proto/Entity
   proto/FetchedDocument
   proto/GetDocflowBatchRequest
   proto/GetDocflowBatchResponse
   proto/GetDocflowEventsRequest
   proto/GetDocflowEventsResponse
   proto/GetDocflowRequest
   proto/GetDocflowsByPacketIdRequest
   proto/GetDocflowsByPacketIdResponse
   proto/InboundInvoiceDocflow
   proto/InboundInvoiceReceiptDocflow
   proto/InvoiceConfirmationDocflow
   proto/InvoiceCorrectionDocumentInfo
   proto/InvoiceCorrectionRequestDocflow
   proto/InvoiceDocumentInfo
   proto/OutboundInvoiceDocflow
   proto/PriceListDocumentInfo
   proto/ReceiptDocflow
   proto/RecipientSignatureDocflow
   proto/RecipientSignatureRejectionDocflow
   proto/RevocationDocflow
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
   proto/XmlBilateralDocflow