DocumentInfo
============

.. code-block:: protobuf

   message DocumentInfo
   {
       optional DocumentType DocumentType = 1 [default = UnknownDocumentType];
       optional DocumentDirection DocumentDirection = 2 [default = UnknownDocumentDirection];
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

Структура представляет данные документа, которые не меняются в течение его жизненного цикла (метаданные). Как часть структуры :doc:`DocumentWithDocflow`, возвращается методами :doc:`../http/GetDocflows`, :doc:`../http/GetDocflowsByPacketId`, :doc:`../http/SearchDocflows`.

-  :doc:`DocumentType` - типа документа.

-  :doc:`DocumentDirection` - направление документа относительно данного ящика (например, исходящий).

-  *IsTest* - признак того, что документ тестовый.

-  *CustomDocumentId* - произвольный идентификатор документа, присвоенный ему во время отправки интеграционным решением.

-  *FromDepartmentId* - идентификатор подразделения-отправителя документа.

-  *ToDepartmentId* - идентификатор подразделения-получателя документа.

-  *CounteragentBoxId* - идентификатор ящика контрагента.

-  :doc:`DocumentDateAndNumber` - дата и номер документа.

- *AttachmentVersion* - идентификатор версии документа. Устарело. Используйте Version.

- *Version* - идентификатор версии документа.

-  Поля, содержащие метаданные документа. В зависимости от типа документа заполняется только одно из полей:

  -  :doc:`BasicDocumentInfo` - для документов XmlTorg12, XmlAcceptanceCertificate, Torg12, AcceptanceCertificate, ProformaInvoice, Torg13.

  -  :doc:`InvoiceInfo <InvoiceDocumentInfo>` - для документов Invoice или InvoiceRevision.

  -  :doc:`InvoiceCorrectionInfo <InvoiceCorrectionDocumentInfo>` - для документов InvoiceCorrection или InvoiceCorrectionRevision.

  -  :doc:`PriceListInfo <PriceListDocumentInfo>` - для документов PriceList.
  
  -  :doc:`ContractInfo <ContractDocumentInfo>` - для документов Contract.

  -  :doc:`SupplementaryAgreementInfo <SupplementaryAgreementDocumentInfo>` - для документов SupplementaryAgreement.

  -  :doc:`utd/docflow/UniversalTransferDocumentInfo` - для документов *UniversalTransferDocument*, *UniversalTransferDocumentRevision*.

  -  :doc:`utd/docflow/UniversalCorrectionDocumentInfo` - для документов *UniversalCorrectionDocument*, *UniversalCorrectionDocumentRevision*.
