Document
========

Структура ``Document`` хранит информацию о документе.

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
        UnknownRoamingNotificationStatus = 0;
        NotificationStatusNone = 1;
        NotificationStatusSuccess = 2;
        NotificationStatusError = 3;
    }

- ``IndexKey`` — уникальный ключ документа, который можно передавать в метод :doc:`../http/GetDocuments` в качестве параметра ``afterIndexKey`` для итерирования по всему отфильтрованному списку.

- ``MessageId`` — идентификатор сообщения, содержащего документ.

- ``EntityId`` — идентификатор соответствующей документу сущности типа ``LetterAttachment`` внутри сообщения.

- ``CreationTimestampTicks`` — время создания документа, представленная структурой :doc:`Timestamp`.

- ``CounteragentBoxId`` — идентификатор ящика контрагента. Значение зависит от направления документа относительно текущего ящика:

	- если документ исходящий — это идентификатор ящика получателя;
	- если документ входящий — идентификатор ящика отправителя;
	- если документ находится в черновиках, поле ``CounteragentBoxId`` может быть пустым.

- ``InitialDocumentIds`` — список идентификаторов исходных документов, к которым привязывается этот документ. Каждый идентификатор представлен структурой :doc:`DocumentId`.

- ``SubordinateDocumentIds`` — список идентификаторов документов, которые ссылаются на этот документ. Каждый идентификатор представлен структурой :doc:`DocumentId`.

- ``Content`` — содержимое документа, представленное структурой :doc:`Content`. При получении документов списком (например, при помощи метода :doc:`../http/GetDocuments`) поле ``Content.Data`` не заполняется из соображений производительности.

- ``FileName`` — имя файла документа при загрузке в Диадок.

- ``IsDeleted`` — флаг, указывающий, что документ был удален.

- ``DepartmentId`` — идентификатор подразделения, в котором находится документ.

- ``IsTest`` — флаг, указывающий, что документ является тестовым и не имеет юридической силы, так как ящик одного из контрагентов тестовый.

- ``FromDepartmentId`` — идентификатор подразделения, из которого отправляется документ.

- ``ToDepartmentId`` — идентификатор подразделения, в которое отправляется документ.

- ``CustomDocumentId`` — идентификатор документа, определяемый внешней системой.

- ``ResolutionStatus`` — статус согласования документа, представленный структурой :doc:`ResolutionStatus`.

- ``RevocationStatus`` — статус аннулирования документа, принимает значения из перечисления :doc:`RevocationStatus`.

- ``SendTimestampTicks`` — время отправки документа, представленное структурой :doc:`Timestamp`.

- ``DeliveryTimestampTicks`` — время доставки документа, представленное структурой :doc:`Timestamp`.

- ``ForwardDocumentEvents`` — список событий пересылки документа третьей стороне. Каждое событие представлено структурой :doc:`ForwardDocumentEvent`. Документ можно переслать нескольким получателям и несколько раз одному получателю.

- ``RoamingNotificationStatus`` — статус доставки в роуминг, принимает значения из перечисления ``RoamingNotificationStatus``:

	- ``RoamingNotificationStatusNone`` — документ не роуминговый или без подтверждения доставки в роуминг;
	- ``RoamingNotificationStatusSuccess`` — документ с подтверждением успешной доставки в роуминг;
	- ``RoamingNotificationStatusError`` — документ с ошибкой доставки в роуминг;
	- ``UnknownRoamingNotificationStatus`` — неизвестный роуминговый статус документа. Может выдаваться, если клиент использует устаревшую версию SDK и не может интерпретировать роуминговый статус документа, переданный сервером.

- ``CustomData`` — список пользовательских данных (:doc:`тегов <../entities/tag>`), привязанных к документу. Каждый тег представлен структурой :doc:`CustomDataItem`.

- ``PacketId`` — идентификатор пакета, в котором находится документ.

- ``DocumentDirection`` — направление движения документа, принимает значения из перечисления :doc:`DocumentDirection`.

- ``LastModificationTimestampTicks`` — время изменения документа, представленное структурой :doc:`Timestamp`.

- ``IsEncryptedContent`` — флаг, указывающий, что содержимое передаваемого документа зашифровано.

- ``SenderSignatureStatus`` — статус подписи отправителя, принимает значения из перечисления :doc:`SenderSignatureStatus`.

- ``IsRead`` — флаг, указывающий, что документ был прочитан сотрудником организации.

- ``RoamingNotificationStatusDescription`` — текстовое описание ошибки, возникшей при доставке документов в роуминг. Поле заполняется, когда статус доставки в роуминг ``RoamingNotificationStatus`` принимает значение ``RoamingNotificationStatusError``.

- ``PacketIsLocked`` — флаг, указывающий, что пакет закрытый.

- ``ResolutionRouteId`` — идентификатор маршрута согласования, на котором находится документ.

- ``ProxySignatureStatus``— статус промежуточной подписи, принимает значения из перечисления :doc:`ProxySignatureStatus`.

- ``TypeNamedId`` — идентификатор типа документа. Список возможных значений можно получить с помощью метода :doc:`../http/GetDocumentTypes`.

- ``Function`` — функция документа. Список возможных значений можно получить с помощью метода :doc:`../http/GetDocumentTypes`.

- ``WorkflowId`` — идентификатор :doc:`вида документооборота <../docflows/Workflows>`, по которому запущен документ.

- ``Title`` — название документа. Например, "Счет-фактура №123 от 26.02.18".

- ``Metadata`` — список метаданных документа. Каждый элемент списка представлен структурой :doc:`../proto/MetadataItem`. Набор возможных значений для конкретного типа можно получить с помощью метода :doc:`../http/GetDocumentTypes`.

- ``RecipientReceiptMetadata`` — состояние извещения о получении документа со стороны получателя. Представлено структурой :doc:`RecipientReceiptMetadata`.

- ``ConfirmationMetadata`` — состояние подтверждения оператором даты отправки или получения документа. Представлено структурой :doc:`ConfirmationMetadata`.

- ``RecipientResponseStatus`` — состояние ответного действия получателя — ответную подпись или подписание ответного титула. Принимает значения из перечисления :doc:`RecipientResponseStatus`.

- ``AmendmentRequestMetadata`` — состояние уведомления об уточнении. Представлено структурой :doc:`AmendmentRequestMetadata`.

- ``Origin``— сущность, из которой был создан документ, например, из черновика или шаблона. Представлено структурой :doc:`Origin`.

- ``EditingSettingId`` — идентификатор :ref:`настройки редактирования <editing_settings>` документа, если он был создан из шаблона с редактируемыми полями.

- ``LockMode``— режим блокировки сообщения, принимает значения из перечисления :doc:`LockMode`. 

- ``SenderReceiptMetadata`` — состояние извещения о получении титула получателя. Представлено структурой :doc:`SenderReceiptMetadata`. 

- ``Version`` — идентификатор версии документа.

- ``LastOuterDocflows``— информация о состоянии внешнего документооборота по документу, представленная структурой :doc:`LastOuterDocflow`.

- ``ProxyBoxId`` — идентификатор ящика промежуточного получателя.

- ``ProxyDepartmentId`` — идентификатор подразделения промежуточного получателя.

- ``DocflowStatus``— информация о статусе документооборота, представленная структурой :doc:`DocflowStatusV3`.

Устаревшие поля
~~~~~~~~~~~~~~~

- ``DocumentType`` — тип документа, принимает значения из перечисления :doc:`obsolete/DocumentType`. Для новых типов значение всегда будет равно ``UnknownDocumentType``. Теперь тип документа возвращается в поле ``TypeNamedId``.

- ``DocumentDate`` — дата формирования документа в формате ДД.ММ.ГГГГ. Может отличаться от даты загрузки документа в Диадок. Теперь дата формирования возвращается в поле ``Metadata``.

- ``DocumentNumber`` — номер документа. Теперь номер возвращается в поле ``Metadata``.

- ``NonformalizedDocumentMetadata`` — дополнительные атрибуты неформализованных документов, представленные структурой :doc:`obsolete/NonformalizedDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata``, ``RecipientReceiptMetadata`` и ``RecipientResponseStatus``.

- ``InvoiceMetadata`` — дополнительные атрибуты счетов-фактур, представленные структурой :doc:`obsolete/InvoiceDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata``, ``RecipientReceiptMetadata``, ``ConfirmationMetadata`` и ``AmendmentRequestMetadata``.

- ``TrustConnectionRequestMetadata`` — дополнительные атрибуты документов типа ``TrustConnectionRequest``, представленные структурой :doc:`obsolete/BilateralDocumentMetadata`. Теперь атрибуты возвращаются в полях  ``Metadata``, ``RecipientResponseStatus``.

- ``Torg12Metadata`` — дополнительные атрибуты товарных накладных ТОРГ-12, представленные структурой :doc:`obsolete/BilateralDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata`` и ``RecipientResponseStatus``.

- ``InvoiceRevisionMetadata`` — дополнительные атрибуты исправлений счетов-фактур, представленные структурой :doc:`obsolete/InvoiceDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata``, ``RecipientReceiptMetadata``, ``ConfirmationMetadata`` и ``AmendmentRequestMetadata``.

- ``InvoiceCorrectionMetadata`` — дополнительные атрибуты корректировочных счетов-фактур, представленные структурой :doc:`obsolete/InvoiceDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata``, ``RecipientReceiptMetadata``, ``ConfirmationMetadata`` и ``AmendmentRequestMetadata``.

- ``InvoiceCorrectionRevisionMetadata`` — дополнительные атрибуты исправлений корректировочных счетов-фактур, представленные структурой :doc:`obsolete/InvoiceDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata``, ``RecipientReceiptMetadata``, ``ConfirmationMetadata`` и ``AmendmentRequestMetadata``.

- ``AcceptanceCertificateMetadata`` — дополнительные атрибуты актов о выполнении работ или оказании услуг, представленные структурой :doc:`obsolete/BilateralDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata`` и ``RecipientResponseStatus``.

- ``ProformaInvoiceMetadata`` — дополнительные атрибуты счетов на оплату, представленные структурой :doc:`obsolete/UnilateralDocumentMetadata`. Теперь атрибуты возвращаются в поле ``Metadata``.

- ``XmlTorg12Metadata`` — дополнительные атрибуты товарных накладных ТОРГ-12 в XML-формате, представленные структурой :doc:`obsolete/BilateralDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata`` и ``RecipientResponseStatus``.

- ``XmlAcceptanceCertificateMetadata`` — дополнительные атрибуты актов о выполнении работ или оказании услуг в XML-формате, представленные структурой :doc:`obsolete/BilateralDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata`` и ``RecipientResponseStatus``.

- ``PriceListMetadata`` — дополнительные атрибуты ценовых листов, представленные структурой :doc:`obsolete/BilateralDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata`` и ``RecipientResponseStatus``.

- ``ReconciliationActMetadata`` — дополнительные атрибуты актов сверки, представленные структурой :doc:`obsolete/BilateralDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata`` и ``RecipientResponseStatus``.

- ``ContractMetadata`` — дополнительные атрибуты договоров, представленные структурой :doc:`obsolete/BilateralDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata`` и ``RecipientResponseStatus``.

- ``Torg13Metadata`` — дополнительные атрибуты накладных ТОРГ-13, представленные структурой :doc:`obsolete/BilateralDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata`` и ``RecipientResponseStatus``.

- ``ServiceDetailsMetadata`` — дополнительные атрибуты детализаций, представленные структурой :doc:`obsolete/UnilateralDocumentMetadata`. Теперь атрибуты возвращаются в поле ``Metadata``.

- ``HasCustomPrintForm`` — флаг, указывающий, что документ имеет нестандартную печатную форму. Значение всегда ``false``. Для выявления нестандартной печатной формы используйте метод :doc:`../http/DetectCustomPrintForms`.

- ``SupplementaryAgreementMetadata`` — дополнительные атрибуты дополнительного соглашения к договору, представленные структурой :doc:`obsolete/BilateralDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata`` и ``RecipientResponseStatus``.

- ``PriceListAgreementMetadata`` — дополнительные атрибуты протоколов согласования цены, представленные структурой :doc:`obsolete/NonformalizedDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata`` и ``RecipientResponseStatus``.

- ``CertificateRegistryMetadata`` — дополнительные атрибуты реестров сертификатов, представленные структурой :doc:`obsolete/NonformalizedDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata`` и ``RecipientResponseStatus``.

- ``UniversalTransferDocumentMetadata`` — дополнительные атрибуты УПД, представленные структурой :doc:`obsolete/UniversalDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata``, ``RecipientResponseStatus``, ``ConfirmationMetadata`` и ``AmendmentRequestMetadata``.

- ``UniversalTransferDocumentRevisionMetadata`` — дополнительные атрибуты исправлений УПД, представленные структурой :doc:`obsolete/UniversalDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata``, ``RecipientResponseStatus``, ``ConfirmationMetadata`` и ``AmendmentRequestMetadata``.

- ``UniversalCorrectionDocumentMetadata`` — дополнительные атрибуты УКД, представленные структурой :doc:`obsolete/UniversalDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata``, ``RecipientResponseStatus``, ``ConfirmationMetadata`` и ``AmendmentRequestMetadata``.

- ``UniversalCorrectionDocumentRevisionMetadata`` — дополнительные атрибуты исправлений УКД, представленные структурой :doc:`obsolete/UniversalDocumentMetadata`. Теперь атрибуты возвращаются в полях ``Metadata``, ``RecipientResponseStatus``, ``ConfirmationMetadata`` и ``AmendmentRequestMetadata``.

- ``AttachmentVersion`` — информация о версии XSD схемы, в соответствии с которой сформирован документ.

----

.. rubric:: Смотри также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetDocument`.