Работа с документами
====================

Для упрощения работы с API существует SDK (C#/C++/Java/COM), скрывающий детали взаимодействия по HTTP и позволяющий работать с API через набор функций.

HTTP-интерфейс
--------------

.. toctree::
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
   :maxdepth: 1
   :titlesonly:

   proto/Content_v2
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
   proto/Official   
   proto/OuterDocflowInfo
   proto/PrepareDocumentsToSignRequest
   proto/PrepareDocumentsToSignResponse
   proto/ResolutionInfo
   proto/ResolutionRequestInfo
   proto/ResolutionRequestDenialInfo
   proto/ResolutionRoute
   proto/ResolutionStatus
   proto/RevocationRequestInfo   
   proto/RoamingNotification
   proto/SignatureRejectionInfo
   proto/Signer
   proto/StructuredDataAttachment
