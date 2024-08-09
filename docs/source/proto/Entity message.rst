Entity
======

Структура ``Entity`` представляет собой сущность, входящую в сообщение или в дополнение к сообщению.

.. code-block:: protobuf

    message Entity {
        required EntityType EntityType = 1;
        required string EntityId = 2;
        optional string AuthorUserId = 33;
        optional string ParentEntityId = 3;
        optional Content Content = 4;
        required AttachmentType AttachmentType = 5;
        optional string FileName = 6;
        optional bool NeedRecipientSignature = 7 [default = false];
        optional string SignerBoxId = 8;
        optional string NotDeliveredEventId = 10;
        optional Documents.Document DocumentInfo = 11;
        optional sfixed64 RawCreationDate = 12 [default = 0];
        optional ResolutionInfo ResolutionInfo = 13;
        optional string SignerDepartmentId = 14;
        optional ResolutionRequestInfo ResolutionRequestInfo = 15;
        optional ResolutionRequestDenialInfo ResolutionRequestDenialInfo = 16;
        optional bool NeedReceipt = 17 [default = false];
        optional string PacketId = 18;
        optional bool IsApprovementSignature = 19 [default = false];
        optional bool IsEncryptedContent = 20 [default = false];
        optional string AttachmentVersion = 21;
        optional ResolutionRouteAssignmentInfo ResolutionRouteAssignmentInfo = 22;
        optional ResolutionRouteRemovalInfo ResolutionRouteRemovalInfo = 23;
        optional CancellationInfo CancellationInfo = 24;
        repeated string Labels = 25;
        optional string Version = 26;
        optional TemplateTransformationInfo TemplateTransformationInfo = 27;
        optional TemplateRefusalInfo TemplateRefusalInfo = 28;
        optional OuterDocflows.OuterDocflowInfo OuterDocflow = 29;
        optional RevocationRequestInfo RevocationRequestInfo = 30;
        optional string ContentTypeId = 31;
        optional PowerOfAttorneyInfo PowerOfAttorneyInfo = 32;
        optional MoveDocumentInfo MoveDocumentInfo = 34;
        optional Docflow.PowerOfAttorneyAttachmentStatus PowerOfAttorneyAttachmentStatus = 35;
    }

    enum EntityType {
        UnknownEntityType = 0;
        Attachment = 1;
        Signature = 2;
    }

    enum AttachmentType {
        UnknownAttachmentType = -1;
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
        RoamingConfirmation = 76;
        PowerOfAttorney = 77;
        PowerOfAttorneyStatus = 78;
    }

    message MoveDocumentInfo {
        required string MovedFromDepartment = 1;
        required string MovedToDepartment = 2; 
    }

- ``EntityType`` — тип сущности, принимает значение из перечисления ``EntityType``:

	- ``UnknownEntityType`` — зарезервированное значение.
	- ``Attachment`` — файл-вложение в сообщении
	- ``Signature`` — электронная подпись под вложением

- ``EntityId`` — уникальный идентификатор сущности.

- ``ParentEntityId`` — идентификатор родительской сущности. Например, для сущности с типом ``Signature`` это будет идентификатор соответствующей сущности с типом ``Attachment``.

- ``Content`` — содержимое сущности, представленное структурой :doc:`Content`. Если у сущности не предусмотрено содержимое, то в поле ``Content`` вернется значение ``null``. Поле ``Content.Data`` содержит массив байтов с данными. Его нужно интерпретировать в зависимости от типа сущности ``EntityType`` и типа вложения ``AttachmentType``:

.. table:: Содержимое Content.Data в зависимости от типа сущности и типа вложения

	+------------------------+--------------------------------------+-------------------------------------------------------------------------------------------+
	| EntityType             | AttachmentType                       | Content.Data                                                                              |
	+========================+======================================+===========================================================================================+
	| Signature              |                                      | Электронная подпись в формате                                                             |
	|                        |                                      | :rfc:`CMS SignedData <5652#section-5>` в                                                  |
	|                        |                                      | в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке |
	+------------------------+--------------------------------------+-------------------------------------------------------------------------------------------+
	| Attachment             | - Nonformalized                      | Двоичное содержимое исходного файла                                                       |
	|                        | - ProformaInvoice                    |                                                                                           |
	|                        | - Torg12                             |                                                                                           |
	|                        | - AcceptanceCertificate              |                                                                                           |
	|                        | - StructuredData                     |                                                                                           |
	|                        | - PriceList                          |                                                                                           |
	|                        +--------------------------------------+-------------------------------------------------------------------------------------------+
	|                        | - Invoice                            | XML-файлы, которыми продавец и покупатель обмениваются                                    |
	|                        | - InvoiceRevision                    | в ходе выставления/получения электронных счетов-фактур                                    |
	|                        | - InvoiceCorrection                  | согласно порядку, утвержденному Минфином России                                           |
	|                        | - InvoiceCorrectionRevision          |                                                                                           |
	|                        | - InvoiceReceipt                     |                                                                                           |
	|                        | - InvoiceConfirmation                |                                                                                           |
	|                        | - InvoiceCorrectionRequest           |                                                                                           |
	|                        +--------------------------------------+-------------------------------------------------------------------------------------------+
	|                        | - XmlTorg12                          | XML-файлы накладных и актов в формате, утвержденном ФНС России                            |
	|                        | - XmlTorg12BuyerTitle                |                                                                                           |
	|                        | - XmlAcceptanceCertificate           |                                                                                           |
	|                        | - XmlAcceptanceCertificateBuyerTitle |                                                                                           |
	|                        +--------------------------------------+-------------------------------------------------------------------------------------------+
	|                        | - TrustConnectionRequest             | XML-файл в формате ``TrustConnectionRequestAttachment``                                   |
	|                        +--------------------------------------+-------------------------------------------------------------------------------------------+
	|                        | - RevocationRequest                  | XML-файл (формат файла)                                                                   |
	|                        +--------------------------------------+-------------------------------------------------------------------------------------------+
	|                        | - XmlSignatureRejection              | XML-файл (формат файла)                                                                   |
	|                        +--------------------------------------+-------------------------------------------------------------------------------------------+
	|                        | - AttachmentComment                  | Строка в кодировке UTF-8                                                                  |
	|                        | - SignatureRequestRejection          |                                                                                           |
	|                        | - DeliveryFailureNotification        |                                                                                           |
	|                        | - Resolution                         |                                                                                           |
	|                        | - ResolutionRequest                  |                                                                                           |
	|                        | - ResolutionRequestDenial            |                                                                                           |
	|                        | - ResolutionRouteAssignment          |                                                                                           |
	|                        | - ResolutionRouteRemoval             |                                                                                           |
	|                        | - RoamingNotification                |                                                                                           |
	|                        +--------------------------------------+-------------------------------------------------------------------------------------------+
	|                        | - SignatureVerificationReport        | Структура :doc:`SignatureVerificationResult`,                                             |
	|                        |                                      | сериализованная в протобуфер                                                              |
	|                        +--------------------------------------+-------------------------------------------------------------------------------------------+
	|                        | - RoamingConfirmation                | XML-файл в формате,                                                                       |
	|                        |                                      | `утвержденном ФНС <https://base.garant.ru/72145228/53f89421bbdaf741eb2d1ecc4ddb4c33>`__.  |
	+------------------------+--------------------------------------+-------------------------------------------------------------------------------------------+

- ``AttachmentType`` — тип вложения. Имеет смысл только для сущностей с типом ``Attachment``. Принимает значение из перечисления ``AttachmentType``:

	- ``UnknownAttachmentType`` — неизвестный тип документа. Возвращается только в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать тип документа, переданный сервером.
	- ``Nonformalized`` — неформализованный документ.
	- ``Invoice`` — счет-фактура.
	- ``InvoiceRevision`` — исправление счета-фактуры.
	- ``InvoiceCorrection`` — корректировочный счет-фактура.
	- ``InvoiceCorrectionRevision`` — исправление корректировочного счета-фактуры.
	- ``InvoiceReceipt`` — извещение о получении счета-фактуры, подтверждения оператора электронного документооборота или уведомления об уточнении счета-фактуры.
	- ``InvoiceConfirmation`` — подтверждение оператора электронного документооборота.
	- ``InvoiceCorrectionRequest`` — уведомление об уточнении счета-фактуры.
	- ``AttachmentComment`` — текстовый комментарий к другой сущности-вложению.
	- ``DeliveryFailureNotification`` — уведомление о невозможности доставки сообщения.
	- ``SignatureRequestRejection`` — отказ в формировании запрошенной подписи.
	- ``SignatureVerificationReport`` — протокол проверки подписи, сформированный Диадоком. Возвращается только в случае, если при проверке были обнаружены ошибки.
	- ``TrustConnectionRequest`` — запрос на инициацию канала обмена документами через Диадок.
	- ``ProformaInvoice`` — счет на оплату.
	- ``Torg12`` — товарная накладная ТОРГ-12.
	- ``AcceptanceCertificate`` — акт о выполнении работ или оказании услуг.
	- ``XmlTorg12`` — товарная накладная ТОРГ-12 в XML-формате, титул продавца.
	- ``XmlTorg12BuyerTitle`` — товарная накладная ТОРГ-12 в XML-формате, титул покупателя.
	- ``XmlAcceptanceCertificate`` — акт о выполнении работ / оказании услуг в XML-формате, титул исполнителя.
	- ``XmlAcceptanceCertificateBuyerTitle`` — акт о выполнении работ / оказании услуг в XML-формате, титул заказчика.
	- ``StructuredData`` — произвольный файл со структурированными данными, описывающими тот или иной документ, представленный в виде печатной формы.
	- ``Resolution`` — информация о статусе согласования документа.
	- ``ResolutionRequest`` — запрос согласования документа.
	- ``ResolutionRequestDenial`` — отказ в запросе подписи документа.
	- ``PriceList`` — ценовой лист.
	- ``PriceListAgreement`` — протокол согласования цены.
	- ``CertificateRegistry`` — реестр сертификатов.
	- ``ReconciliationAct`` — акт сверки.
	- ``Contract`` — договор.
	- ``Torg13`` — накладная ТОРГ-13.
	- ``ServiceDetails`` — детализация.
	- ``Receipt`` — извещение о получении.
	- ``XmlSignatureRejection`` — формализованный отказ в подписи.
	- ``RevocationRequest`` — предложение об аннулировании.
	- ``RoamingNotification`` — роуминговая квитанция.
	- ``SupplementaryAgreement`` — дополнительное соглашение к договору.
	- ``CustomData`` — произвольные данные к документу.
	- ``MoveDocument`` — информация о перемещении документа в подразделение.
	- ``ResolutionRouteAssignment`` — информация о запуске документа по маршруту согласования.
	- ``ResolutionRouteRemoval`` — информация о снятии документа с маршрута согласования.
	- ``Title`` — титул документа. Возвращается для всех типов документов, кроме типов от 0 (``AttachmentType=Nonformalized``) до 51 (``AttachmentType=UniversalCorrectionDocumentBuyerTitle``). Это сделано для сохранения обратной совместимости: для первых титулов (титулов отправителя) с типами от ``Nonformalized`` до ``UniversalCorrectionDocumentBuyerTitle`` возвращается соответствующее значение, например, ``Invoice`` для счета-фактуры и т.п.
	- ``Cancellation`` — информация об отмене сущности, которая указана родительской по отношению к данной.
	- ``Edition`` — информация о редактировании контента документа, который указан родительским по отношению к данной сущности.
	- ``DeletionRestoration`` — восстановление удаленного документа.
	- ``TemplateTransformation`` — информация о трансформации.
	- ``TemplateRefusal`` — информация об отклонении или отзыве шаблона.
	- ``OuterDocflow`` — информация о внешнем документообороте.
	- ``RoamingConfirmation`` — подтверждение оператора, отправленное в роуминг или полученное из роуминга.
	- ``PowerOfAttorney`` — информация о машиночитаемой доверенности.
	- ``PowerOfAttorneyStatus`` — статус проверки машиночитаемой доверенности.

	Неизвестные типы обрабатываются как ``Nonformalized``.

- ``FileName`` — исходное имя файла. Возвращается только для сущностей с типом ``Attachment``.

- ``NeedRecipientSignature`` — флаг, обозначающий запрос подписи получателя под данной сущностью. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``Nonformalized``.

- ``SignerBoxId`` — идентификатор ящика автора данной подписи. Возвращается только для сущностей с типом ``Signature``.

- ``NotDeliveredEventId`` — идентификатор сообщения или патча, который не удалось доставить (например, из-за некорректности одной или нескольких подписей в нем). Получить недоставленный кусок сообщения можно с помощью метода :doc:`../http/GetEvent`, передав в качестве параметра ``eventId`` значение ``NotDeliveredEventId``. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``DeliveryFailureNotification``.

- ``DocumentInfo`` — расширенная информация о документе, представляемом данной сущностью, представленная структурой :doc:`Document`. Возвращается только для сущностей с типом ``Attachment`` со следующими типами вложений:

	- ``Nonformalized``
	- ``Invoice``
	- ``InvoiceRevision``
	- ``InvoiceCorrection``
	- ``InvoiceCorrectionRevision``
	- ``TrustConnectionRequest``
	- ``ProformaInvoice``
	- ``Torg12``
	- ``AcceptanceCertificate``
	- ``XmlTorg12``
	- ``XmlAcceptanceCertificate``
	- ``PriceList``
	- ``PriceListAgreement``
	- ``CertificateRegistry``
	- ``ReconciliationAct``
	- ``Contract``
	- ``Torg13``
	- ``ServiceDetails``
	- ``Title``
	- ``UniversalTransferDocument``
	- ``UniversalCorrectionDocument``
	- ``UniversalTransferDocumentRevision``

- ``RawCreationDate`` — время создания сущности, целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001.

- ``ResolutionInfo`` — информация о согласовании, представленная структурой :doc:`ResolutionInfo`. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``Resolution``.

- ``SignerDepartmentId`` — идентификатор подразделения, в котором лежала сущность в момент подписания. Возвращается только для сущностей с типом ``Signature``.

- ``ResolutionRequestInfo`` — информация о запросе согласования, представленная структурой :doc:`ResolutionRequestInfo`. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``ResolutionRequest``.

- ``ResolutionRequestDenialInfo`` — информация об отказе в запросе подписи, представленная структурой :doc:`ResolutionRequestDenialInfo`. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``ResolutionRequestDenial``.

- ``NeedReceipt`` — флаг, указывающий, что от получателя требуется сформировать извещение о получении данного документа. Возвращается только для сущностей с типом ``Attachment``.

- ``IsApprovementSignature`` — флаг, указывающий, что подпись является :ref:`согласующей <resolution_signature>`. Возвращается только для сущностей с типом ``Signature``.

- ``IsEncryptedContent`` — флаг, указывающий, зашифрован ли контент документа.

- ``AttachmentVersion`` — информация о версии XSD схемы, в соответствии с которой сформирована данная сущность. Поле устарело, используйте значение поля ``Version``.

- ``ResolutionRouteAssignmentInfo`` — информация о запуске документа по маршруту согласования, представленная структурой :doc:`ResolutionRouteAssignmentInfo <ResolutionRouteInfo>`.  Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``ResolutionRouteAssignment``.

- ``ResolutionRouteRemovalInfo`` — информация о снятии документа с маршрута согласования, представленная структурой :doc:`ResolutionRouteRemovalInfo <ResolutionRouteInfo>`. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``ResolutionRouteRemoval``.

- ``CancellationInfo`` — информация об отмене сущности, представленная структурой :doc:`CancellationInfo`. Отмененной является сущность, которая указана родительской по отношению к данной. Например, это может быть идентификатор запроса на согласование. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``Cancellation``.

- ``Labels`` — список :doc:`меток <../entities/label>` сущности.

- ``Version`` — идентификатор версии документа.

- ``TemplateTransformationInfo`` — информация о документе, созданном на основе шаблона, представленная структурой :doc:`TemplateTransformationInfo`. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``TemplateTransformation``.

- ``TemplateRefusalInfo`` — информация об отклонении или отзыве шаблона, представленная структурой :doc:`TemplateRefusalInfo`. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``TemplateRefusal``.

- ``OuterDocflow`` — информация о внешнем документообороте, например, о статусе обработки документа с маркированными товарами в ГИС МТ «Честный ЗНАК». Представлена структурой :doc:`OuterDocflowInfo`. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``OuterDocflow``.

- ``RevocationRequestInfo`` — информация о соглашении об аннулировании, представленная структурой :doc:`RevocationRequestInfo <RevocationRequestInfo_Entity>`. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``RevocationRequest``.

- ``ContentTypeId`` — уникальный идентификатор контента документа. ``ContentTypeId`` будет единым для документов с одинаковой структурой и одинаковыми правилами обработки. Идентификатор будет свой для каждого типа документа, титула и служебного документа. Например, УПД 820 формата с функцией СЧФДОП будет иметь ``ContentTypeId=utd820_schfdop_orig_t1_05_01_01`` для первого титула и ``ContentTypeId=utd820_schfdop_t2_05_01_01`` для второго титула, а для отказа в подписи в формате уведомления об уточнении ``ContentTypeId=signature_rejection_02``.

- ``PowerOfAttorneyInfo`` — информация о машиночитаемой доверенности и статусе ее проверки, представленная структурой :doc:`PowerOfAttorneyInfo`. Возвращается только для сущностей с типом ``Attachment`` с типами вложения ``PowerOfAttorney`` и ``PowerOfAttorneyStatus``. Статус проверки машиночитаемой доверенности ``PowerOfAttorneyValidationStatus`` возвращается только для сущностей с типом ``Attachment`` с типом вложения ``PowerOfAttorneyStatus``. Для машиночитаемой доверенности в поле ``ParentEntityId`` возвращается:
 
	- для вложения с типом ``PowerOfAttorney`` — идентификатор подписи,
	- для вложения с типом ``PowerOfAttorneyStatus`` — идентификатор МЧД.

- ``AuthorUserId`` — идентификатор пользователя-автора сущности. Возвращается только для сущностей с типом ``Signature`` и ``Attachment`` со следующими типами вложений:

	- ``Resolution``
	- ``ResolutionRequest``
	- ``ResolutionRequestDenial``
	- ``ResolutionRouteAssignment``
	- ``ResolutionRouteRemoval``
	- ``OuterDocflow``
	- ``TemplateTransformation``
	- ``TemplateRefusal``
	- ``CustomData``
	- ``Edition``
	- ``MoveDocument``
	- ``RevocationRequest``

- ``MoveDocumentInfo`` — информация о перемещении документа в другое подразделение. Возвращается только для сущностей с типом ``Attachment`` с типом вложения ``MoveDocument``. Представлена структурой ``MoveDocumentInfo`` с полями:

	- ``MovedFromDepartment`` — подразделение, в которое переместили документ.
	- ``MovedToDepartment`` — подразделение, из которого переместили документ.

- ``PowerOfAttorneyAttachmentStatus`` — статус приложенности машиночитаемой доверенности (МЧД) к подписи, представленный структурой :doc:`PowerOfAttorneyAttachmentStatus`. Возвращается только для сущностей с типом ``Signature``.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Message`
	- в структуре :doc:`MessagePatch`