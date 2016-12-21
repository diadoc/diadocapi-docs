Document
========

.. code-block:: protobuf

    message Document {
        optional string IndexKey = 1;
        required string MessageId = 2;
        required string EntityId = 3;
        required sfixed64 CreationTimestampTicks = 4;
        optional string CounteragentBoxId = 5;
        optional DocumentType DocumentType = 6 [default = UnknownDocumentType];
        repeated DocumentId InitialDocumentIds = 7;
        repeated DocumentId SubordinateDocumentIds = 8;
        optional Content Content = 9;
        optional string FileName = 10;
        optional string DocumentDate = 11;
        optional string DocumentNumber = 12;
        optional NonformalizedDocument.NonformalizedDocumentMetadata NonformalizedDocumentMetadata = 13;
        optional InvoiceDocument.InvoiceMetadata InvoiceMetadata = 14;
        optional BilateralDocument.TrustConnectionRequestMetadata TrustConnectionRequestMetadata = 15;
        optional BilateralDocument.BasicDocumentMetadata Torg12Metadata = 16;
        optional InvoiceDocument.InvoiceRevisionMetadata InvoiceRevisionMetadata = 17;
        optional InvoiceDocument.InvoiceCorrectionMetadata InvoiceCorrectionMetadata = 18;
        optional InvoiceDocument.InvoiceCorrectionRevisionMetadata InvoiceCorrectionRevisionMetadata = 19;
        optional AcceptanceCertificateDocument.AcceptanceCertificateMetadata AcceptanceCertificateMetadata = 20;
        optional UnilateralDocument.ProformaInvoiceMetadata ProformaInvoiceMetadata = 21;
        optional BilateralDocument.BasicDocumentMetadata XmlTorg12Metadata = 22;
        optional BilateralDocument.BasicDocumentMetadata XmlAcceptanceCertificateMetadata = 23;
        optional bool IsDeleted = 24 [default = false];
        optional string DepartmentId = 25;
        optional bool IsTest = 26 [default = false];
        optional string FromDepartmentId = 27;
        optional string ToDepartmentId = 28;
        optional BilateralDocument.PriceListMetadata PriceListMetadata = 29;
        optional string CustomDocumentId = 30;
        optional ResolutionStatus ResolutionStatus = 31;
        optional RevocationStatus RevocationStatus = 32 [default = UnknownRevocationStatus];
        optional sfixed64 SendTimestampTicks = 33;
        optional sfixed64 DeliveryTimestampTicks = 34;
        repeated ForwardDocumentEvent ForwardDocumentEvents = 35;
        optional BilateralDocument.NonformalizedDocumentMetadata PriceListAgreementMetadata = 36;
        optional BilateralDocument.NonformalizedDocumentMetadata CertificateRegistryMetadata = 37;
        optional BilateralDocument.BilateralDocumentMetadata ReconciliationActMetadata = 38;
        optional BilateralDocument.ContractMetadata ContractMetadata = 39;
        optional BilateralDocument.BasicDocumentMetadata Torg13Metadata = 40;
        optional UnilateralDocument.ServiceDetailsMetadata ServiceDetailsMetadata = 41;
        optional RoamingNotificationStatus RoamingNotificationStatus = 42 [default = UnknownRoamingNotificationStatus];
        optional bool HasCustomPrintForm = 43 [default = false];
        repeated CustomDataItem CustomData = 44;
        optional string PacketId = 45;
        optional DocumentDirection DocumentDirection = 46 [default = UnknownDocumentDirection];
        optional sfixed64 LastModificationTimestampTicks = 47;
        optional bool IsEncryptedContent = 48;
        optional SenderSignatureStatus SenderSignatureStatus = 49 [default = UnknownSenderSignatureStatus];
        optional BilateralDocument.SupplementaryAgreementMetadata SupplementaryAgreementMetadata = 50;
        optional bool IsRead = 51 [default = false];
        optional string RoamingNotificationStatusDescription = 52;
        optional BilateralDocument.UniversalTransferDocumentMetadata UniversalTransferDocumentMetadata = 53;
    }

    enum RevocationStatus {
        UnknownRevocationStatus = 0; // Reserved status to report to legacy clients for newly introduced statuses
        RevocationStatusNone = 1;
        RevocationIsRequestedByMe = 2;
        RequestsMyRevocation = 3;
        RevocationAccepted = 4;
        RevocationRejected = 5;
    }

    enum RoamingNotificationStatus {
        UnknownRoamingNotificationStatus = 0; // Reserved status to report to legacy clients for newly introduced statuses
        NotificationStatusNone = 1;
        NotificationStatusSuccess = 2;
        NotificationStatusError = 3;
    }

    enum SenderSignatureStatus {
        UnknownSenderSignatureStatus = 0; // Reserved status to report to legacy clients for newly introduced statuses
        WaitingForSenderSignature = 1;
        SenderSignatureUnchecked = 2;
        SenderSignatureCheckedAndValid = 3;
        SenderSignatureCheckedAndInvalid = 4;
    }

Структура данных *Document* содержит инфофрмацию об одном документе в Диадоке, которую можно получить, например, при помощи метода :doc:`../http/GetDocument`:

-  *IndexKey* - уникальный ключ документа, который можно передавать в метод :doc:`../http/GetDocuments` в качестве параметра *afterIndexKey* для итерирования по всему отфильтрованному списку.

-  *MessageId* - идентификатор сообщения, содержащего данный документ.

-  *EntityId* - идентификатор соответствующей документу сущности типа *LetterAttachment* внутри сообщения.

-  *CreationTimestampTicks* - :doc:`метка времени <Timestamp>` создания данного документа.

-  *CounteragentBoxId* - идентификатор Диадок-ящика контрагента по данному документу.

    В случае исходящего документа - это идентификатор ящика получателя, в случае входящего документа - идентификатор ящика отправителя;

    Если документ находится в черновиках, то поле *CounteragentBoxId* может быть не заполнено.

-  *DocumentType* - тип документа, принимает одно из значений перечислимого типа :doc:`DocumentType`. В зависимости от типа документа заполняется одно из полей *Document.XxxMetadata*.

-  *InitialDocumentIds* - список идентификаторов документов, на которые ссылается данный;

    каждый такой идентификатор задается структурой :doc:`DocumentId`.

-  *SubordinateDocumentIds* - список идентификаторов документов, которые ссылаются на данный;

    каждый такой идентификатор задается структурой :doc:`DocumentId`.

-  *Content* - содержимое документа.

    Поле *Content.Size* определяет размер содержимого в байтах.

    Поле *Content.Data* содержит собственно данные.

    При получении документов списком (например, при помощи метода :doc:`../http/GetDocuments`) поле *Content.Data* не заполняется из соображений производительности.

-  *FileName* - имя файла документа, которое у него было при загрузке в Диадок.

-  *DocumentDate* - дата формирования документа в формате ДД.ММ.ГГГГ; может отличаться от даты загрузки его в Диадок.

-  *DocumentNumber* - номер документа.

-  *IsDeleted* - флаг, показывающий, был ли удален данный документ.

-  *DepartmentId* - идентификатор подразделения, в котором находится документ.

-  *IsTest* - флаг, показывающий, что данный документ является тестовым и не имеет юридической силы, т.к. один из контрагентов не присоединился  к регламенту Диадока.

-  *FromDepartmentId* - идентификатор подразделения, из которого отправляется документ.

-  *ToDepartmentId* - идентификатор подразделения, в которое отправляется документ.

-  *CustomDocumentId* - идентификатор документа, определяемый внешней системой.
   
-  *IsEncryptedContent* - флаг, показывающий, что контент передаваемого документа зашифрован.

-  :doc:`NonformalizedDocumentMetadata` - дополнительные атрибуты специфичные для неформализованных документов.

-  :doc:`InvoiceMetadata <InvoiceDocumentMetadata>` - дополнительные атрибуты специфичные для счетов-фактур.

-  :doc:`InvoiceRevisionMetadata <InvoiceDocumentMetadata>` - дополнительные атрибуты специфичные для исправлений счетов-фактур.

-  :doc:`InvoiceCorrectionMetadata <InvoiceDocumentMetadata>` - дополнительные атрибуты специфичные для корректировочных счетов-фактур.

-  :doc:`InvoiceCorrectionRevisionMetadata <InvoiceDocumentMetadata>` - дополнительные атрибуты специфичные для исправлений корректировочных счетов-фактур.

-  :doc:`TrustConnectionRequestMetadata <BilateralDocumentMetadata>` - дополнительные атрибуты специфичные для документов типа TrustConnectionRequest.

-  :doc:`Torg12Metadata <BilateralDocumentMetadata>` - дополнительные атрибуты специфичные для товарных накладных ТОРГ-12.

-  :doc:`AcceptanceCertificateMetadata <BilateralDocumentMetadata>` - дополнительные атрибуты специфичные для актов о выполнении работ (оказании услуг).

-  :doc:`ProformaInvoiceMetadata <UnilateralDocumentMetadata>` - дополнительные атрибуты специфичные для счетов на оплату.

-  :doc:`XmlTorg12Metadata <BilateralDocumentMetadata>` - дополнительные атрибуты специфичные для товарных накладных ТОРГ-12 в XML-формате.

-  :doc:`XmlAcceptanceCertificateMetadata <BilateralDocumentMetadata>` - дополнительные атрибуты специфичные для актов о выполнении работ (оказании услуг) в XML-формате.

-  :doc:`PriceListMetadata <BilateralDocumentMetadata>` - дополнительные атрибуты специфичные для ценовых листов.

-  :doc:`PriceListAgreementMetadata <NonformalizedDocumentMetadata>` - дополнительные атрибуты специфичные для протоколов согласования цены.

-  :doc:`CertificateRegistryMetadata <NonformalizedDocumentMetadata>` - дополнительные атрибуты специфичные для реестров сертификатов.

-  :doc:`ReconciliationActMetadata <BilateralDocumentMetadata>` - дополнительные атрибуты специфичные для актов сверки.

-  :doc:`ContractMetadata <BilateralDocumentMetadata>` - дополнительные атрибуты специфичные для договоров.

-  :doc:`Torg13Metadata <BilateralDocumentMetadata>` - дополнительные атрибуты специфичные для накладных ТОРГ-13.

-  :doc:`SupplementaryAgreementMetadata <BilateralDocumentMetadata>` - дополнительные атрибуты специфичные для типа документа дополнительное соглашение к договору.

-  :doc:`ResolutionStatus <ResolutionStatus>` - текущий статус согласования данного документа.

-  :doc:`ServiceDetailsMetadata <UnilateralDocumentMetadata>` - дополнительные атрибуты специфичные для детализаций.

-  :doc:`UniversalTransferDocumentMetadata <BilateralDocumentMetadata>` - Дополнительные атрибуты, специфичные для универсального передаточного документа

-  *RevocationStatus* - статус аннулирования документа. Возможные значения:

   -  *RevocationStatusNone* (документ не аннулирован, и не было предложений об аннулировании)

   -  *RevocationIsRequestedByMe* (отправлено исходящее предложение об аннулировании документа)

   -  *RequestsMyRevocation* (получено входящее предложение об аннулировании документа)

   -  *RevocationAccepted* (документ аннулирован)

   -  *RevocationRejected* (получен или отправлен отказ от предложения об аннулировании документа)

   -  *UnknownRevocationStatus* (неизвестный статус аннулирования документа; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать статус аннулирования документа, переданный сервером)

-  *SendTimestampTicks* - Необязательная :doc:`метка времени <Timestamp>` отправки данного документа.

-  *DeliveryTimestampTicks* - Необязательная :doc:`метка времени <Timestamp>` доставки данного документа.

-  *ForwardDocumentEvents* - Список :doc:`событий пересылки <ForwardDocumentEvent>` данного документа третьей стороне. Документ может быть переслан нескольким получателям, а также - несколько раз одному получаетлю.

-  *RoamingNotificationStatus* - статус доставки в роуминг. Возможные значения:

   -  *RoamingNotificationStatusNone* (документ не роуминговый, или документ без подтверждения доставки в роуминг)

   -  *RoamingNotificationStatusSuccess* (документ с подтверждением успешной доставки в роуминг)

   -  *RoamingNotificationStatusError* (документ с ошибкой доставки в роуминг)
   
   -  *UnknownRoamingNotificationStatus* (неизвестный роуминговый статус документа; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать роуминговый статус документа, переданный сервером)

-  *HasCustomPrintForm* - флаг, показывающий, что данный документ имеет нестандартную печатную форму. Скачать печатную форму документа можно при помощи метода :doc:`../http/GeneratePrintForm`.

- *IsRead* - флаг, указывающий на то, что документ был прочитан сотрудником организации.

- *RoamingNotificationStatusDescription* - текстовое описание ошибки при доставке документов в роуминг. Обычно это поле заполняется, когда статус доставки в роуминг *RoamingNotificationStatus* имеет значение *RoamingNotificationStatusError*.