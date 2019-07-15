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
   http/GenerateSenderTitleXml
   http/GenerateRecipientTitleXml
   http/GenerateAcceptanceCertificateXmlForBuyer
   http/GenerateAcceptanceCertificateXmlForSeller
   http/GenerateDocumentProtocol
   http/GenerateDocumentZip
   http/GenerateForwardedDocumentProtocol
   http/GenerateDocumentReceiptXml
   http/GeneratePrintForm
   http/GeneratePrintFormFromAttachment
   http/GenerateRevocationRequestXml
   http/GenerateSignatureRejectionXml
   http/GenerateTorg12XmlForBuyer
   http/GenerateTorg12XmlForSeller
   http/GetDocument
   http/GetDocuments
   http/GetDocumentsByMessageId
   http/GetForwardedDocumentEvents
   http/GenerateForwardedDocumentPrintForm
   http/GetForwardedEntityContent
   http/GetForwardedDocuments
   http/GetGeneratedPrintForm
   http/MoveDocuments
   http/ParseTitleXml
   http/ParseAcceptanceCertificateSellerTitleXml
   http/ParseAcceptanceCertificateBuyerTitleXml
   http/ParseRevocationRequestXml
   http/ParseSignatureRejectionXml
   http/ParseTorg12SellerTitleXml
   http/ParseTorg12BuyerTitleXml
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
   proto/NonformalizedAttachment
   proto/NonformalizedDocumentMetadata
   proto/Official   
   proto/PrepareDocumentsToSignRequest
   proto/PrepareDocumentsToSignResponse
   proto/PriceListAttachment
   proto/ReconciliationActAttachment
   proto/Resolution
   proto/ResolutionRequest
   proto/ResolutionRequestDenial
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
