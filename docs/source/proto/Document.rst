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
        optional BilateralDocument.BilateralDocumentMetadata ReconciliationActMetadata = 38;
        optional BilateralDocument.ContractMetadata ContractMetadata = 39;
        optional BilateralDocument.BasicDocumentMetadata Torg13Metadata = 40;
        optional UnilateralDocument.ServiceDetailsMetadata ServiceDetailsMetadata = 41;
        optional RoamingNotificationStatus RoamingNotificationStatus = 42 [default = UnknownRoamingNotificationStatus];
        optional bool HasCustomPrintForm = 43 [default = false]; // Deprecated
        repeated CustomDataItem CustomData = 44;
        optional string PacketId = 45;
        optional DocumentDirection DocumentDirection = 46 [default = UnknownDocumentDirection];
        optional sfixed64 LastModificationTimestampTicks = 47;
        optional bool IsEncryptedContent = 48;
        optional SenderSignatureStatus SenderSignatureStatus = 49 [default = UnknownSenderSignatureStatus];
        optional BilateralDocument.SupplementaryAgreementMetadata SupplementaryAgreementMetadata = 50;
        optional bool IsRead = 51 [default = false];
        optional string RoamingNotificationStatusDescription = 52;
        optional bool PacketIsLocked = 53 [default = false];
        optional NonformalizedDocumentMetadata PriceListAgreementMetadata = 54;
        optional NonformalizedDocumentMetadata CertificateRegistryMetadata = 55;
        optional UniversalTransferDocumentMetadata UniversalTransferDocumentMetadata = 56;
        optional UniversalTransferDocumentRevisionMetadata UniversalTransferDocumentRevisionMetadata = 57;
        optional UniversalCorrectionDocumentMetadata UniversalCorrectionDocumentMetadata = 58;
        optional UniversalCorrectionDocumentRevisionMetadata UniversalCorrectionDocumentRevisionMetadata = 59;
        optional string ResolutionRouteId = 60 [default = ""];
        optional string AttachmentVersion = 61;
        optional ProxySignatureStatus ProxySignatureStatus = 62 [default = UnknownProxySignatureStatus];

        required string TypeNamedId = 63;
        required string Function = 64;
        required int32 WorkflowId = 65;
        required string Title = 66;
        repeated Events.MetadataItem Metadata = 67;
        required RecipientReceiptMetadata RecipientReceiptMetadata = 68;
        required ConfirmationMetadata ConfirmationMetadata = 69;
        required RecipientResponseStatus RecipientResponseStatus = 70 [default = RecipientResponseStatusUnknown];
        required AmendmentRequestMetadata AmendmentRequestMetadata = 71;
        optional Origin Origin = 72;
        optional string EditingSettingId = 73 [default = ""];
        required LockMode LockMode = 74;
        required SenderReceiptMetadata SenderReceiptMetadata = 75;
        required string Version = 76;
        repeated LastOuterDocflow LastOuterDocflows = 77;
        optional string ProxyBoxId = 78;
        optional string ProxyDepartmentId = 79;
        required DocflowStatusV3 DocflowStatus = 80; 
    }

    enum RoamingNotificationStatus {
        UnknownRoamingNotificationStatus = 0; // Reserved status to report to legacy clients for newly introduced statuses
        NotificationStatusNone = 1;
        NotificationStatusSuccess = 2;
        NotificationStatusError = 3;
    }

Структура данных *Document* содержит информацию об одном документе в Диадоке, которую можно получить, например, при помощи метода :doc:`../http/GetDocument`:

-  *IndexKey* - уникальный ключ документа, который можно передавать в метод :doc:`../http/GetDocuments` в качестве параметра *afterIndexKey* для итерирования по всему отфильтрованному списку.

-  *MessageId* - идентификатор сообщения, содержащего данный документ.

-  *EntityId* - идентификатор соответствующей документу сущности типа *LetterAttachment* внутри сообщения.

-  *CreationTimestampTicks* - :doc:`метка времени <Timestamp>` создания данного документа.

-  *CounteragentBoxId* - идентификатор Диадок-ящика контрагента по данному документу.

    В случае исходящего документа - это идентификатор ящика получателя, в случае входящего документа - идентификатор ящика отправителя;

    Если документ находится в черновиках, то поле *CounteragentBoxId* может быть не заполнено.

-  *DocumentType* (устаревшее, см. *TypeNamedId*) - тип документа, принимает одно из значений перечислимого типа :doc:`DocumentType`. В зависимости от типа документа заполняется одно из полей *Document.XxxMetadata*. Для новых типов значение всегда будет равно `UnknownDocumentType`.

-  *InitialDocumentIds* - список идентификаторов документов, на которые ссылается данный;

    каждый такой идентификатор задается структурой :doc:`DocumentId`.

-  *SubordinateDocumentIds* - список идентификаторов документов, которые ссылаются на данный;

    каждый такой идентификатор задается структурой :doc:`DocumentId`.

-  *Content* - содержимое документа.

    Поле *Content.Size* определяет размер содержимого в байтах.

    Поле *Content.Data* содержит собственно данные.

    При получении документов списком (например, при помощи метода :doc:`../http/GetDocuments`) поле *Content.Data* не заполняется из соображений производительности.

-  *FileName* - имя файла документа, которое у него было при загрузке в Диадок.

-  *DocumentDate* (устаревшее, см. *Metadata*) - дата формирования документа в формате ДД.ММ.ГГГГ; может отличаться от даты загрузки его в Диадок.

-  *DocumentNumber* (устаревшее, см. *Metadata*) - номер документа.

-  *IsDeleted* - флаг, показывающий, был ли удален данный документ.

-  *DepartmentId* - идентификатор подразделения, в котором находится документ.

-  *IsTest* - флаг, показывающий, что данный документ является тестовым и не имеет юридической силы, т.к. один из контрагентов не присоединился к регламенту Диадока.

-  *FromDepartmentId* - идентификатор подразделения, из которого отправляется документ.

-  *ToDepartmentId* - идентификатор подразделения, в которое отправляется документ.

-  *CustomDocumentId* - идентификатор документа, определяемый внешней системой.
   
-  *IsEncryptedContent* - флаг, показывающий, что контент передаваемого документа зашифрован.

-  :doc:`SenderSignatureStatus` - статус подписи отправителя.

-  :doc:`NonformalizedDocumentMetadata` (устаревшее, см. *Metadata*, *RecipientReceiptMetadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для неформализованных документов.

-  :doc:`InvoiceMetadata <InvoiceDocumentMetadata>` (устаревшее, см. *Metadata*, *RecipientReceiptMetadata*, *ConfirmationMetadata* и *AmendmentRequestMetadata*) - дополнительные атрибуты специфичные для счетов-фактур.

-  :doc:`InvoiceRevisionMetadata <InvoiceDocumentMetadata>` (устаревшее, см. *Metadata*, *RecipientReceiptMetadata*, *ConfirmationMetadata* и *AmendmentRequestMetadata*) - дополнительные атрибуты специфичные для исправлений счетов-фактур.

-  :doc:`InvoiceCorrectionMetadata <InvoiceDocumentMetadata>` (устаревшее, см. *Metadata*, *RecipientReceiptMetadata*, *ConfirmationMetadata* и *AmendmentRequestMetadata*) - дополнительные атрибуты специфичные для корректировочных счетов-фактур.

-  :doc:`InvoiceCorrectionRevisionMetadata <InvoiceDocumentMetadata>` (устаревшее, см. *Metadata*, *RecipientReceiptMetadata*, *ConfirmationMetadata* и *AmendmentRequestMetadata*) - дополнительные атрибуты специфичные для исправлений корректировочных счетов-фактур.

-  :doc:`TrustConnectionRequestMetadata <BilateralDocumentMetadata>` (устаревшее, см. *Metadata*, *RecipientResponseStatus*) - дополнительные атрибуты специфичные для документов типа TrustConnectionRequest.

-  :doc:`Torg12Metadata <BilateralDocumentMetadata>` (устаревшее, см. *Metadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для товарных накладных ТОРГ-12.

-  :doc:`AcceptanceCertificateMetadata <BilateralDocumentMetadata>` (устаревшее, см. *Metadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для актов о выполнении работ (оказании услуг).

-  :doc:`ProformaInvoiceMetadata <UnilateralDocumentMetadata>` (устаревшее, см. *Metadata*) - дополнительные атрибуты специфичные для счетов на оплату.

-  :doc:`XmlTorg12Metadata <BilateralDocumentMetadata>` (устаревшее, см. *Metadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для товарных накладных ТОРГ-12 в XML-формате.

-  :doc:`XmlAcceptanceCertificateMetadata <BilateralDocumentMetadata>` (устаревшее, см. *Metadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для актов о выполнении работ (оказании услуг) в XML-формате.

-  :doc:`PriceListMetadata <BilateralDocumentMetadata>` (устаревшее, см. *Metadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для ценовых листов.

-  :doc:`PriceListAgreementMetadata <NonformalizedDocumentMetadata>` (устаревшее, см. *Metadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для протоколов согласования цены.

-  :doc:`CertificateRegistryMetadata <NonformalizedDocumentMetadata>` (устаревшее, см. *Metadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для реестров сертификатов.

-  :doc:`ReconciliationActMetadata <BilateralDocumentMetadata>` (устаревшее, см. *Metadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для актов сверки.

-  :doc:`ContractMetadata <BilateralDocumentMetadata>` (устаревшее, см. *Metadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для договоров.

-  :doc:`Torg13Metadata <BilateralDocumentMetadata>` (устаревшее, см. *Metadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для накладных ТОРГ-13.

-  :doc:`SupplementaryAgreementMetadata <BilateralDocumentMetadata>` (устаревшее, см. *Metadata* и *RecipientResponseStatus*) - дополнительные атрибуты специфичные для типа документа дополнительное соглашение к договору.

-  :doc:`ResolutionStatus <ResolutionStatus>` - текущий статус согласования данного документа.

-  :doc:`ServiceDetailsMetadata <UnilateralDocumentMetadata>` (устаревшее, см. *Metadata*) - дополнительные атрибуты специфичные для детализаций.

-  :doc:`UniversalTransferDocumentMetadata <utd/UniversalDocumentMetadata>` (устаревшее, см. *Metadata*, *RecipientResponseStatus*, *ConfirmationMetadata* и *AmendmentRequestMetadata*) - дополнительные атрибуты, специфичные для УПД

-  :doc:`UniversalTransferDocumentRevisionMetadata <utd/UniversalDocumentMetadata>` (устаревшее, см. *Metadata*, *RecipientResponseStatus*, *ConfirmationMetadata* и *AmendmentRequestMetadata*) - дополнительные атрибуты, специфичные для исправлений УПД

-  :doc:`UniversalCorrectionDocumentMetadata <utd/UniversalDocumentMetadata>` (устаревшее, см. *Metadata*, *RecipientResponseStatus*, *ConfirmationMetadata* и *AmendmentRequestMetadata*) - дополнительные атрибуты, специфичные для УКД

-  :doc:`UniversalCorrectionDocumentRevisionMetadata <utd/UniversalDocumentMetadata>` (устаревшее, см. *Metadata*, *RecipientResponseStatus*, *ConfirmationMetadata* и *AmendmentRequestMetadata*) - дополнительные атрибуты, специфичные для исправлений УКД

-  :doc:`RevocationStatus` - статус аннулирования документа.

-  *SendTimestampTicks* - Необязательная :doc:`метка времени <Timestamp>` отправки данного документа.

-  *DeliveryTimestampTicks* - Необязательная :doc:`метка времени <Timestamp>` доставки данного документа.

-  *ForwardDocumentEvents* - Список :doc:`событий пересылки <ForwardDocumentEvent>` данного документа третьей стороне. Документ может быть переслан нескольким получателям, а также - несколько раз одному получателю.

-  *RoamingNotificationStatus* - статус доставки в роуминг. Возможные значения:

   -  *RoamingNotificationStatusNone* (документ не роуминговый, или документ без подтверждения доставки в роуминг)

   -  *RoamingNotificationStatusSuccess* (документ с подтверждением успешной доставки в роуминг)

   -  *RoamingNotificationStatusError* (документ с ошибкой доставки в роуминг)
   
   -  *UnknownRoamingNotificationStatus* (неизвестный роуминговый статус документа; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать роуминговый статус документа, переданный сервером)

-  *HasCustomPrintForm* - флаг, показывающий, что данный документ имеет нестандартную печатную форму. Свойство более **не поддерживается**. Значение всегда *false*. В случае необходимости используйте метод :doc:`../http/DetectCustomPrintForms`.

- *IsRead* - флаг, указывающий на то, что документ был прочитан сотрудником организации.

- *RoamingNotificationStatusDescription* - текстовое описание ошибки при доставке документов в роуминг. Обычно это поле заполняется, когда статус доставки в роуминг *RoamingNotificationStatus* имеет значение *RoamingNotificationStatusError*.

- *ResolutionRouteId* - идентификатор маршрута согласования, на котором находится документ (если документ находится на маршруте согласования).

- *AttachmentVersion* - информация о версии XSD схемы, в соответствии с которой сформирован документ. Устарело. Используйте Version.

- :doc:`ProxySignatureStatus` - статус промежуточной подписи.

- *TypeNamedId* - строковый идентификатор типа документа. Его следует использовать вместо свойства *DocumentType*. Может принимать значения "Nonformalized", "Invoice", "Torg12", "XmlTorg12" и другие. Полный список возможных значений можно получить с помощью метода :doc:`../http/GetDocumentTypes`.

- *Function* — функция документа.

 Для документов типа УПД (``UniversalTransferDocument``) и ИУПД  (``UniversalTransferDocumentRevision``) может принимать значения:
 
 - "СЧФ"
 - "ДОП"
 - "СЧФДОП"
 - "СвРК"
 - "СвЗК"
	
 Для документов типа УКД (``UniversalCorrectionDocument``) и ИУКД (``UniversalCorrectionDocumentRevision``) может принимать значения:
 
 - "КСЧФ"
 - "ДИС"
 - "КСЧФДИС"
 - "СвИСРК"
 - "СвИСЗК"
	
 Для всех остальных типов принимает значение ``default``. 

- *WorkflowId* - числовой идентификатор типа документооброта, по которому запущен документ. Более подробную информацию см. :doc:`../proto/DocumentWorkflow`.

- *Title* - название документа. Например, "Счет-фактура №123 от 26.02.18".

- *Metadata* - массив пар "ключ-значение", определямых типом документа. Примеры возможных значения ключей: "FileName", "DocumentDate", "DocumentNumber" и другие. Более подробную информацию см. :doc:`../proto/MetadataItem`. Набор возможных значений для конкретного типа можно узнать с помощью метода :doc:`../http/GetDocumentTypes`.

- :doc:`RecipientReceiptMetadata <RecipientReceiptMetadata>` - свойство, отвечающее за состояние извещения о получении документа со стороны получателя.

- :doc:`ConfirmationMetadata <ConfirmationMetadata>` - свойство, отвечающее за состояние подтверждения оператором даты отправки/получения документа. Актуально, например, для счетов-фактур и УПД/УКД с некоторыми функциями.

- :doc:`RecipientResponseStatus <RecipientResponseStatus>` - свойство, отвечающее за состояние ответного действия получателя - ответную подпись или подписание ответного титула.

- :doc:`AmendmentRequestMetadata <AmendmentRequestMetadata>` - свойство, отвечающее за состояние уведомления об уточнении. Актуально, например, для счетов-фактур, УПД и некоторых версий актов и накладных.

- :doc:`Origin <Origin>` - свойство, позволяющее узнать, из какой сущности был создан документ. Например, из черновика или шаблона.

- *EditingSettingId* - необязательный идентификатор настройки документа, если он был создан из шаблона с возможностью редактирования полей.

- :doc:`LockMode <LockMode>` - режим блокировки сообщения.

- :doc:`SenderReceiptMetadata <SenderReceiptMetadata>` - свойство, отвечающее за состояние извещения о получении титула получателя.

- *Version* - идентификатор версии документа.

- :doc:`LastOuterDocflows <LastOuterDocflow>` - информация о состоянии внешнего документооборота по документу, например, о статусе обработки документа с маркированными товарами в ГИС МТ "Честный ЗНАК".

- *ProxyBoxId* - идентификатор ящика промежуточного получателя.

- *ProxyDepartmentId* - идентификатор подразделения промежуточного получателя.

- :doc:`DocflowStatus <DocflowStatusV3>` - информация о статусе документооборота.

.. warning::
    Свойства *NonformalizedDocumentMetadata*, *InvoiceMetadata*, *InvoiceRevisionMetadata*, *InvoiceCorrectionMetadata*, *InvoiceCorrectionRevisionMetadata*, *TrustConnectionRequestMetadata*, *Torg12Metadata*, *AcceptanceCertificateMetadata*, *ProformaInvoiceMetadata*, *XmlTorg12Metadata*, *XmlAcceptanceCertificateMetadata*, *PriceListMetadata*, *PriceListAgreementMetadata*, *CertificateRegistryMetadata*, *ReconciliationActMetadata*, *ContractMetadata*, *Torg13Metadata*, *SupplementaryAgreementMetadata*, *ServiceDetailsMetadata*, *UniversalTransferDocumentMetadata*, *UniversalTransferDocumentRevisionMetadata*, *UniversalCorrectionDocumentMetadata* и *UniversalCorrectionDocumentRevisionMetadata*, *HasCustomPrintForm* считаются **устаревшими** и **не рекомендованы** к использованию. В будущем они будут удалены.
