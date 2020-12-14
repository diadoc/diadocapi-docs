Entity
======

.. code-block:: protobuf

    message Entity {
        optional EntityType EntityType = 1 [default = UnknownEntityType];
        required string EntityId = 2;
        optional string ParentEntityId = 3;
        optional Content Content = 4;   // значение отсутствует тогда и только тогда, когда у сущности не предусмотрен контент
        optional AttachmentType AttachmentType = 5 [default = UnknownAttachmentType];
        optional string FileName = 6;
        optional bool NeedRecipientSignature = 7 [default = false];
        optional string SignerBoxId = 8;
        optional string NotDeliveredEventId = 10;
        optional Documents.Document DocumentInfo = 11;
        optional sfixed64 RawCreationDate = 12 [default = 0];
        optional ResolutionInfo ResolutionInfo = 13; // заполняется только для вложений с типом AttachmentType.Resolution
        optional string SignerDepartmentId = 14;     // заполняется только для вложений с типом EntityType.Signature
        optional ResolutionRequestInfo ResolutionRequestInfo = 15;  // заполняется только для вложений с типом AttachmentType.ResolutionRequest
        optional ResolutionRequestDenialInfo ResolutionRequestDenialInfo = 16;  // заполняется только для вложений с типом AttachmentType.ResolutionRequestDenial
        optional bool NeedReceipt = 17 [default = false];						// заполняется только для вложений с типом EntityType.Attachment
        optional string PacketId = 18;
        optional bool IsApprovementSignature = 19 [default = false];   // заполняется только для вложений с типом EntityType.Signature
        optional bool IsEncryptedContent = 20 [default = false];
        optional string AttachmentVersion = 21;
        optional ResolutionRouteAssignmentInfo ResolutionRouteAssignmentInfo = 22; // заполняется только для вложений с типом AttachmentType.ResolutionRouteAssignment
        optional ResolutionRouteRemovalInfo ResolutionRouteRemovalInfo = 23; // заполняется только для вложений с типом AttachmentType.ResolutionRouteRemoval
        optional CancellationInfo CancellationInfo = 24;  // заполняется только для вложений с типом AttachmentType.Cancellation
        repeated string Labels = 25;
        optional string Version = 26;
        optional TemplateTransformationInfo TemplateTransformationInfo = 27;
        optional TemplateRefusalInfo TemplateRefusalInfo = 28;
        optional OuterDocflowInfo OuterDocflow = 29;   // заполняется только для вложений с типом AttachmentType.OuterDocflow
        optional RevocationRequestInfo RevocationRequestInfo = 30; // заполняется только для вложений с типом AttachmentType.RevocationRequest
    }

    enum EntityType {
        UnknownEntityType = 0;  // Reserved type to report to legacy clients for newly introduced entity types
        Attachment = 1;
        Signature = 2;
    }

    enum AttachmentType {
        UnknownAttachmentType = -1; // Reserved attachment type to report to legacy clients for newly introduced attachment types
        Nonformalized = 0;
        Invoice = 1;
        InvoiceReceipt = 2;
        InvoiceConfirmation = 3;
        InvoiceCorrectionRequest = 4;
        AttachmentComment = 5;
        DeliveryFailureNotification = 6;
        SignatureRequestRejection = 8;
        SignatureVerificationReport = 10;
        TrustConnectionRequest = 11;
        Torg12 = 12;
        InvoiceRevision = 13;
        InvoiceCorrection = 14;
        InvoiceCorrectionRevision = 15;
        AcceptanceCertificate = 16;
        StructuredData = 17;
        ProformaInvoice = 18;
        XmlTorg12 = 19;
        XmlAcceptanceCertificate = 20;
        XmlTorg12BuyerTitle = 21;
        XmlAcceptanceCertificateBuyerTitle = 22;
        Resolution = 23;
        ResolutionRequest = 24;
        ResolutionRequestDenial = 25;
        PriceList = 26;
        Receipt = 27;
        XmlSignatureRejection = 28;
        RevocationRequest = 29;
        PriceListAgreement = 30;
        CertificateRegistry = 34;
        ReconciliationAct = 35;
        Contract = 36;
        Torg13 = 37;
        ServiceDetails = 38;
        RoamingNotification = 39;
        SupplementaryAgreement = 40;
        UniversalTransferDocument = 41;
        UniversalTransferDocumentBuyerTitle = 42;
        UniversalTransferDocumentRevision = 45;
        UniversalCorrectionDocument = 49;
        UniversalCorrectionDocumentRevision = 50;
        UniversalCorrectionDocumentBuyerTitle = 51;
        CustomData = 64;
        MoveDocument = 65;
        ResolutionRouteAssignment = 66;
        ResolutionRouteRemoval = 67;
        Title = 68;
        Cancellation = 69;
        Edition = 71;
        DeletionRestoration = 72;
        TemplateTransformation = 73;
        TemplateRefusal = 74;
        OuterDocflow = 75;
        // Неизвестные типы должны обрабатываться как Nonformalized
    }

Структура данных *Entity* представляет одну сущность, входящую в сообщение или в дополнение к сообщению. Содержится в структурах :doc:`Message` и :doc:`MessagePatch`.

-  *EntityType* определяет тип сущности; возможные варианты:

   -  *Attachment* (файл-вложение в сообщении),
   
   -  *Signature* (ЭП под вложением).

-  *EntityId* - уникальный идентификатор сущности.

-  *ParentEntityId* - идентификатор родительской сущности. Например, для сущности *Signature* это будет идентификатор соответствующей сущности *Attachment*.

-  *AttachmentType* определяет тип вложения (имеет смысл только для сущностей типа *Attachment*), возможные варианты:

   -  *UnknownAttachmentType* (неизвестный тип документа; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать тип документа, переданный сервером),

   -  *Nonformalized* (неформализованный документ),
   
   -  *Invoice* (счет-фактура),
   
   -  *InvoiceRevision* (исправление счета-фактуры),
   
   -  *InvoiceCorrection* (корректировочный счет-фактура),
   
   -  *InvoiceCorrectionRevision* (исправление корректировочного счета-фактуры),
   
   -  *InvoiceReceipt* (извещение о получении счета-фактуры, подтверждения оператора электронного документооборота или уведомления об уточнении счета-фактуры),
   
   -  *InvoiceConfirmation* (подтверждение оператора электронного документооборота),
   
   -  *InvoiceCorrectionRequest* (уведомление об уточнении счета-фактуры),
   
   -  *AttachmentComment* (текстовый комментарий к другой сущности-вложению),
   
   -  *DeliveryFailureNotification* (уведомление о невозможности доставки сообщения),
   
   -  *SignatureRequestRejection* (отказ в формировании запрошенной подписи),
   
   -  *SignatureVerificationReport* (протокол проверки подписи, сформированный Диадоком),
   
   -  *TrustConnectionRequest* (запрос на инициацию канала обмена документами через Диадок),
   
   -  *ProformaInvoice* (счет на оплату),
   
   -  *Torg12* (товарная накладная ТОРГ-12),
   
   -  *AcceptanceCertificate* (акт о выполнении работ / оказании услуг),
   
   -  *XmlTorg12* (товарная накладная ТОРГ-12 в XML-формате, титул продавца),
   
   -  *XmlTorg12BuyerTitle* (товарная накладная ТОРГ-12 в XML-формате, титул покупателя),
   
   -  *XmlAcceptanceCertificate* (акт о выполнении работ / оказании услуг в XML-формате, титул исполнителя),
   
   -  *XmlAcceptanceCertificateBuyerTitle* (акт о выполнении работ / оказании услуг в XML-формате, титул заказчика),
   
   -  *StructuredData* (произвольный файл со структурированными данными, описывающими тот или иной документ, представленный в виде печатной формы),
   
   -  *Resolution* (информация о статусе согласования документа),
   
   -  *ResolutionRequest* (запрос согласования документа),
   
   -  *ResolutionRequestDenial* (отказ в запросе подписи документа),
   
   -  *PriceList* (ценовой лист),
   
   -  *PriceListAgreement* (протокол согласования цены),
   
   -  *CertificateRegistry* (реестр сертификатов),
   
   -  *ReconciliationAct* (акт сверки),
   
   -  *Contract* (договор),
   
   -  *Torg13* (накладная ТОРГ-13),
   
   -  *ServiceDetails* (детализация),
   
   -  *Receipt* (извещение о получении),
   
   -  *XmlSignatureRejection* (формализованный отказ в подписи),
   
   -  *RevocationRequest* (предложение об аннулировании).
   
   -  *RoamingNotification* (роуминговая квитанция).
   
   -  *SupplementaryAgreement* (дополнительное соглашение к договору).
   
   -  *CustomData* (произвольные данные к документу).
   
   -  *MoveDocument* (информация о перемещении документа в подразделение).
   
   -  *ResolutionRouteAssignment* (информация о запуске документа по маршруту согласования).

   -  *ResolutionRouteRemoval* (информация о снятии документа с маршрута согласования).
   
   -  *Title* (титул документа; возвращается для всех вновь добавляемых типов документов, для сохранения обратной совместимости для первых титулов типов от Invoice до UniversalCorrectionDocumentRevision возвращается соответствующее значение),

   -  *Cancellation* (информация об отмене сущности, которая указана родительской по отношению к данной).

   -  *Edition* (информация о редактировании контента документа, который указан родительским по отношению к данной сущности).
   
   -  *DeletionRestoration* (восстановление удалённого документа).

   -  *TemplateTransformation* (информация о трансформации)
   
   -  *TemplateRefusal* (информация об отклонении или отзыве шаблона)

-  *Content* - содержимое сущности (подробнее см. описание структуры :doc:`Content`).
   
   -  Поле Content.Size определяет размер содержимого в байтах,
   
   -  Поле Content.Data, если присутствует, содержит собственно данные. Этот массив байтов следует интерпретировать в зависимости от типа сущности *EntityType* и типа вложения *AttachmentType*:

   -  Содержимое сущности типа *Signature* представляет собой ЭП в формате CMS SignedData в DER-кодировке,
   
   -  Для сущностей типа *Attachment/Nonformalized*, *Attachment/ProformaInvoice*, *Attachment/Torg12*, *Attachment/AcceptanceCertificate*, *Attachment/StructuredData*, *Attachment/PriceList* - это просто двоичное содержимое исходного файла,
   
   -  Сущности типа *Attachment* с типами вложений *Invoice*, *InvoiceRevision*, *InvoiceCorrection*, *InvoiceCorrectionRevision*, *InvoiceReceipt*, *InvoiceConfirmation*, *InvoiceCorrectionRequest* представляют собой XML-файлы, которыми продавец и покупатель обмениваются в ходе выставления/получения электронных счетов-фактур согласно порядку, утвержденному Минфином России,
   
   -  Сущности типа *Attachment* с типами вложений *XmlTorg12*, *XmlTorg12BuyerTitle*, *XmlAcceptanceCertificate*, *XmlAcceptanceCertificateBuyerTitle* представляют собой XML-файлы накладных и актов в формате, утвержденном ФНС России,
   
   -  Содержимое сущности типа *Attachment/TrustConnectionRequest* представляет собой XML-файл в формате *TrustConnectionRequestAttachment*,
   
   -  Содержимое сущности типа *Attachment/RevocationRequest* представляет собой XML-файл (формат файла),
   
   -  Содержимое сущности типа *Attachment/XmlSignatureRejection* представляет собой XML-файл (формат файла),
   
   -  Содержимое сущности типа *Attachment/RoamingNotification* представляет собой сериализованную в протобуфер структуру *RoamingNotification*,
   
   -  Для сущностей типа *Attachment* и типов вложений *AttachmentComment*, *SignatureRequestRejection*, *DeliveryFailureNotification*, *Resolution*, *ResolutionRequest*, *ResolutionRequestDenial*, *ResolutionRouteAssignment*, *ResolutionRouteRemoval* массив байтов Content.Data следует интерпретировать как строку в кодировке UTF-8,
   
   -  Наконец, у сущности типа *Attachment/SignatureVerificationReport* массив байтов Content.Data представляет собой сериализованную в протобуфер структуру *SignatureVerificationResult*.

-  *FileName* - для сущности типа *Attachment* это исходное имя файла. Для остальных типов сущностей это поле не заполняется.

-  *NeedRecipientSignature* - флаг, обозначающий запрос подписи получателя под данной сущностью; имеет смысл только для сущностей типа Attachment с типом вложения Nonformalized.

-  *SignerBoxId* - для сущности типа Signature это идентификатор ящика автора данной подписи. Для остальных типов сущностей это поле не заполняется.

-  *NotDeliveredEventId* - это идентификатор сообщения или патча, который не удалось доставить (например, из-за некорректности одной или нескольких подписей в нем). Получить недоставленный кусок сообщения можно при помощи метода :doc:`../http/GetEvent`, передав ему в качестве параметра eventId значение *NotDeliveredEventId*. Данное поле заполняется только у сущности типа Attachment с типом вложения *DeliveryFailureNotification*.

-  *DocumentInfo* - для сущности типа Attachment содержит расширенную информацию о документе, представляемом данной сущностью, в виде структуры данных :doc:`Document`. Заполняется только у сущностей типа *Attachment/Nonformalized*, *Attachment/Invoice*, *Attachment/InvoiceRevision*, *Attachment/InvoiceCorrection*, *Attachment/InvoiceCorrectionRevision*, *Attachment/TrustConnectionRequest*, *Attachment/ProformaInvoice*, *Attachment/Torg12*, *Attachment/AcceptanceCertificate*, *Attachment/XmlTorg12*, *Attachment/XmlAcceptanceCertificate*, *Attachment/PriceList*, *Attachment/PriceListAgreement*, *Attachment/CertificateRegistry*, *Attachment/ReconciliationAct*, *Attachment/Contract*, *Attachment/Torg13*, *Attachment/ServiceDetails*, *Attachment/Title*

-  *RawCreationDate* - :doc:`метка времени <Timestamp>` создания сущности.

-  *ResolutionInfo* - информация о согласовании в виде структуры данных :doc:`ResolutionInfo <Resolution>`.

-  *SignerDepartmentId* - для сущности типа Signature это идентификатор подразделения в котором лежала сущность в момент подписания. Для остальных типов сущностей это поле не заполняется.

-  *ResolutionRequestInfo* - информация о запросе согласования в виде структуры данных :doc:`ResolutionRequestInfo <ResolutionRequest>`.

-  *ResolutionRequestDenialInfo* - информация об отказе в запросе подписи в виде структуры данных :doc:`ResolutionRequestDenialInfo <ResolutionRequestDenial>`.

-  *IsApprovementSignature* - является ли подпись согласующей или обычной; заполняется только для сущностей типа Signature. Подробнее про согласующие подписи см. :doc:`DocumentSignature <DocumentSignature>`.

-  *IsEncryptedContent* - флаг, указывающий зашифрован ли контент документа.

- *AttachmentVersion* - информация о версии XSD схемы, в соответствии с которой сформирована данная сущность.

-  *ResolutionRouteAssignmentInfo* - информация о запуске документа по маршруту согласования в виде структуры данных :doc:`ResolutionRouteAssignmentInfo <ResolutionRouteInfo>`.

-  *ResolutionRouteRemovalInfo* - информация о снятии документа с маршрута согласования в виде структуры данных :doc:`ResolutionRouteRemovalInfo <ResolutionRouteInfo>`.

- *CancellationInfo* - информация об отмене сущности в виде структуры данных :doc:`CancellationInfo <CancellationInfo>`. Отменённой является сущность, которая указана родительской по отношению к данной. Например, это может быть идентификатор запроса на согласование.

- *Labels* - :doc:`метки сущности <../proto/Labels>`.

- *Version* - идентификатор версии документа.

- *TemplateTransformationInfos* - содержит информацию о документе, созданном на основе шаблона. Будет заполняться для AttachmentType=TemplateTransformation.

- :doc:`TemplateRefusalInfo` - содержит информацию об отклонении или отзыве шаблона. Будет заполняться для AttachmentType=TemplateRefusal.

- :doc:`OuterDocflow <OuterDocflowInfo>` - содержит информацию о внешнем документообороте, например, о статусе обработки документа с маркированными товарами в ГИС МТ "Честный ЗНАК". Будет заполняться для AttachmentType=OuterDocflow.

- :doc:`RevocationRequestInfo <RevocationRequestInfo_Entity>` - содержит информацию о соглашении об аннулировании.
