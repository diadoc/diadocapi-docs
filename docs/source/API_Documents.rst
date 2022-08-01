Работа с документами
====================

Для упрощения работы с API существует SDK (C#/C++/Java/COM), скрывающий детали взаимодействия по HTTP и позволяющий работать с API через набор функций.

HTTP-интерфейс
--------------

.. toctree::
   :name: toc3
   :maxdepth: 1
   :titlesonly:

   http/Delete
   http/DetectCustomPrintForms
   http/ForwardDocument
   http/GenerateTitleXml
   http/GenerateDocumentProtocol
   http/GenerateDocumentZip
   http/GenerateForwardedDocumentPrintForm
   http/GenerateForwardedDocumentProtocol
   http/GenerateReceiptXml
   http/GeneratePrintForm
   http/GeneratePrintFormFromAttachment
   http/GenerateRevocationRequestXml
   http/GenerateSignatureRejectionXml
   http/GetDocument
   http/GetDocuments
   http/GetDocumentsByMessageId
   http/GetForwardedDocumentEvents
   http/GetResolutionRoutesForOrganization
   http/GetForwardedEntityContent
   http/GetForwardedDocuments
   http/GetGeneratedPrintForm
   http/MoveDocuments
   http/ParseTitleXml
   http/ParseRevocationRequestXml
   http/ParseSignatureRejectionXml
   http/PrepareDocumentsToSign
   http/RecycleDraft
   http/Restore
   http/ShelfDownload
   http/ShelfUpload
   http/SendDraft

Структуры данных
----------------

.. toctree::
   :name: toc4
   :maxdepth: 1
   :titlesonly:

   proto/AcceptanceCertificateAttachment
   proto/AcceptanceCertificate552Info
   proto/AcceptanceCertificateInfo
   proto/BasicDocumentAttachment
   proto/BilateralDocumentMetadata
   proto/Content_v2
   proto/ContractAttachment
   proto/CustomDataPatch
   proto/Document
   proto/DocumentList
   proto/DocumentSignature   
   proto/DocumentProtocol
   proto/DocumentSenderSignature
   proto/DocumentZipGenerationResult
   proto/DocumentsMoveOperation
   proto/DraftToSend
   proto/ForwardedDocument
   proto/LastOuterDocflow
   proto/NonformalizedAttachment
   proto/NonformalizedDocumentMetadata
   proto/Official   
   proto/OuterDocflowInfo
   proto/PrepareDocumentsToSignRequest
   proto/PrepareDocumentsToSignResponse
   proto/PriceListAttachment
   proto/ReconciliationActAttachment
   proto/Resolution
   proto/ResolutionRequest
   proto/ResolutionRequestDenial
   proto/ResolutionRoute
   proto/ResolutionStatus
   proto/RevocationRequestInfo   
   proto/RoamingNotification
   proto/ServiceDetailsAttachment
   proto/SignatureRejectionInfo
   proto/Signer
   proto/StructuredDataAttachment
   proto/Torg12Info
   proto/TovTorgInfo
   proto/Torg13Attachment
   proto/TrustConnectionRequestAttachment
   proto/UnilateralDocumentMetadata
   proto/XmlDocumentAttachment
