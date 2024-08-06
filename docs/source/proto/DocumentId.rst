DocumentId
==========

Структура ``DocumentId`` представляет собой идентификатор документа:

.. code-block:: protobuf

    message DocumentId
    {
        required string MessageId = 1;
        required string EntityId = 2;
    }

- ``MessageId`` — идентификатор сообщения, в котором содержится документ.
- ``EntityId`` — идентификатор сущности документа внутри сообщения.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Content_v3`
	- в структуре :doc:`Counteragent`
	- в структуре :doc:`CounteragentInfo`
	- в структуре :doc:`DocflowEventV3`
	- в структуре :doc:`Document`
	- в структуре :doc:`DocumentAttachment`
	- в структуре :doc:`DocumentLinks`
	- в структуре :doc:`DocumentPatchedContent <PrepareDocumentsToSignResponse>`
	- в структуре :doc:`DocumentsMoveOperation`
	- в структуре :doc:`DocumentToPatch <PrepareDocumentsToSignRequest>`
	- в структуре :doc:`DocumentWithDocflowV3`
	- в структуре :doc:`DraftDocumentToPatch <PrepareDocumentsToSignRequest>`
	- в структуре :ref:`EditDocumentPacketCommand`
	- в структуре :doc:`ForwardedDocumentId <ForwardedDocument>`
	- в структуре :doc:`GetDocflowRequest`
	- в структуре :doc:`OrganizationWithCounteragentStatus <GetOrganizationsByInnListResponse>`
	- в структуре :doc:`TemplateTransformationInfo <DocumentInfoV3>`
	- в структуре :doc:`TemplateTransformationInfo`
	- в структуре ``CustomPrintFormDetectionRequest``, используемой в теле запроса метода :doc:`../http/DetectCustomPrintForms`
	- в структуре ``ForwardDocumentRequest``, используемой в теле запроса метода :doc:`../http/ForwardDocument`
	- в структуре ``AcquireCounteragentResultV2``, возвращаемой методом :doc:`../http/AcquireCounteragentResult`
	- в структуре ``CustomPrintFormDetectionItemResult``, возвращаемой методом :doc:`../http/DetectCustomPrintForms`
	- в структуре ``ForwardDocumentResponse``, возвращаемой методом :doc:`../http/ForwardDocument`
	- в устаревшей структуре :doc:`obsolete/AcceptanceCertificateAttachment`
	- в устаревшей структуре :doc:`obsolete/BasicDocumentAttachment`
	- в устаревшей структуре :doc:`obsolete/ContractAttachment`
	- в устаревшей структуре :doc:`obsolete/DocflowEvent`
	- в устаревшей структуре :doc:`obsolete/DocumentWithDocflow`
	- в устаревшей структуре :doc:`obsolete/EncryptedInvoiceAttachment`
	- в устаревшей структуре :doc:`obsolete/EncryptedXmlDocumentAttachment`
	- в устаревшей структуре :doc:`obsolete/NonformalizedAttachment`
	- в устаревшей структуре :doc:`obsolete/PriceListAttachment`
	- в устаревшей структуре :doc:`obsolete/ReconciliationActAttachment`
	- в устаревшей структуре :doc:`obsolete/ServiceDetailsAttachment`
	- в устаревшей структуре :doc:`obsolete/SupplementaryAgreementAttachment`
	- в устаревшей структуре :doc:`obsolete/Torg13Attachment`
	- в устаревшей структуре :doc:`obsolete/XmlDocumentAttachment`
	- в структуре ``AcquireCounteragentResult``, возвращаемой устаревшей версией метода :doc:`../http/obsolete/AcquireCounteragentResult`