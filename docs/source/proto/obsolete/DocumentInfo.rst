DocumentInfo
============

.. warning::
	Структура относится к устаревшей версии Docflow API. Вместо нее используется структура :doc:`../../proto/DocumentInfoV3` последней версии :doc:`../../Docflow API` — V3.

Структура ``DocumentInfo`` представляет собой метаданные документа — данные, которые не меняются в течение его жизненного цикла.

.. code-block:: protobuf

   message DocumentInfo
   {
       optional DocumentType DocumentType = 1;
       optional DocumentDirection DocumentDirection = 2;
       optional bool IsTest = 3;
       optional string CustomDocumentId = 4;
       optional string FromDepartmentId = 5;
       optional string ToDepartmentId = 6;
       optional string CounteragentBoxId = 7;
       optional DocumentDateAndNumber DocumentDateAndNumber = 8;
       optional BasicDocumentInfo BasicDocumentInfo = 9;
       optional InvoiceDocumentInfo InvoiceInfo = 10;
       optional InvoiceCorrectionDocumentInfo InvoiceCorrectionInfo = 11;
       optional PriceListDocumentInfo PriceListInfo = 12;
       optional ContractDocumentInfo ContractInfo = 13;
       optional SupplementaryAgreementDocumentInfo SupplementaryAgreementInfo = 14;
       optional UniversalTransferDocumentInfo UniversalTransferDocumentInfo = 15;
       optional UniversalCorrectionDocumentInfo UniversalCorrectionDocumentInfo = 16;
       optional string AttachmentVersion = 17;
       required string Version = 18;
    }

- ``DocumentType`` — тип документа, представленный структурой :doc:`DocumentType`.
- ``DocumentDirection`` — направление документа относительно данного ящика (входящий или исходящий), представленный структурой :doc:`../DocumentDirection`.
- ``IsTest`` — признак того, что документ тестовый.
- ``CustomDocumentId`` — идентификатор документа, определяемый внешней системой.
- ``FromDepartmentId`` — идентификатор подразделения-отправителя документа.
- ``ToDepartmentId`` — идентификатор подразделения-получателя документа.
- ``CounteragentBoxId`` — идентификатор ящика контрагента.
- ``DocumentDateAndNumber`` — дата и номер документа, представленные структурой :doc:`../DocumentDateAndNumber`.
- ``AttachmentVersion`` — идентификатор версии документа. Поле устарело, вместо него используйте поле ``Version``.
- ``Version`` — идентификатор версии документа.

-  Поля, содержащие метаданные документа. В зависимости от типа документа заполняется только одно из полей:

   - ``BasicDocumentInfo`` — поле со структурой :doc:`BasicDocumentInfo` для документов ``XmlTorg12``, ``XmlAcceptanceCertificate``, ``Torg12``, ``AcceptanceCertificate``, ``ProformaInvoice``, ``Torg13``.
   - ``InvoiceInfo`` — поле со структурой :doc:`InvoiceDocumentInfo` для документов ``Invoice`` или ``InvoiceRevision``.
   - ``InvoiceCorrectionInfo`` — поле со структурой :doc:`InvoiceCorrectionDocumentInfo` для документов ``InvoiceCorrection`` или ``InvoiceCorrectionRevision``.
   - ``PriceListInfo`` — поле со структурой :doc:`PriceListDocumentInfo` для документов ``PriceList``.
   - ``ContractInfo`` — поле со структурой :doc:`ContractDocumentInfo` для документов ``Contract``.
   - ``SupplementaryAgreementInfo`` — поле со структурой :doc:`SupplementaryAgreementDocumentInfo` для документов ``SupplementaryAgreement``.
   - ``UniversalTransferDocumentInfo`` — поле со структурой :doc:`UniversalTransferDocumentInfo` для документов ``UniversalTransferDocument``, ``UniversalTransferDocumentRevision``.
   - ``UniversalCorrectionDocumentInfo`` — поле со структурой :doc:`UniversalCorrectionDocumentInfo` для документов ``UniversalCorrectionDocument``, ``UniversalCorrectionDocumentRevision``.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocumentWithDocflow`.

*Руководства:*
	- :doc:`../../Docflow API`