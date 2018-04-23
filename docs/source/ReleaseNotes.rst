﻿История изменений API
=====================

v.1.51.3 - 23.04.2018
---------------------

- Расширена структура контракта :doc:`Document <proto/Document>`. Добавлено свойство :doc:`Origin <proto/Origin>`, позволяющее узнать, из какого черновика или шаблона был создан документ.

v.1.51.2 - 16.04.2018
---------------------

- Расширена структура контракта :doc:`MessagePatchToPost <proto/MessagePatchToPost>`. Добавлен необязательный список операций *EditingPatches* для редактирования контента документа.


v.1.51.1 - 12.04.2018
---------------------

- Расширена структура контракта :doc:`TemplateDocumentAttachment <proto/TemplateDocumentAttachment>`. Добавлен необязательный признак *NeedRecipientSignature*, обозначающий запрос подписи получателя под отправляемым документом, созданным из шаблона, а также необязательный идентификатор настройки редактирования содержимого документа :doc:`EditingSettingId <proto/TemplateDocumentAttachment>`.


v.1.51 - 29.03.2018
-------------------

Добавлены :doc:`метки <Labels>`.

Свойство *Labels* добавлено в структуры:

- :doc:`Entity <proto/Entity message>`
- :doc:`ReceiptAttachment <proto/MessagePatchToPost>`
- :doc:`CorrectionRequestAttachment <proto/MessagePatchToPost>`
- :doc:`DocumentSignature <proto/MessagePatchToPost>`
- :doc:`SignatureVerification <proto/MessagePatchToPost>`
- :doc:`ResolutionAttachment <proto/Resolution>`
- :doc:`ResolutionRequestAttachment <proto/ResolutionRequest>`
- :doc:`ResolutionRouteAssignment <proto/MessagePatchToPost>`
- :doc:`ResolutionRequestCancellationAttachment <proto/ResolutionRequest>`
- :doc:`ResolutionRequestDenialAttachment <proto/ResolutionRequestDenial>`
- :doc:`RequestedSignatureRejection <proto/MessagePatchToPost>`
- :doc:`RevocationRequestAttachment <proto/MessagePatchToPost>`
- :doc:`XmlSignatureRejectionAttachment <proto/MessagePatchToPost>`


v.1.50 - 26.02.2018
-------------------

- Расширена структура контракта :doc:`proto/Document`. Добавились свойства для универсальной работы с документом. Свойства *NonformalizedDocumentMetadata*, *InvoiceMetadata*, *InvoiceRevisionMetadata*, *InvoiceCorrectionMetadata*, *InvoiceCorrectionRevisionMetadata*, *TrustConnectionRequestMetadata*, *Torg12Metadata*, *AcceptanceCertificateMetadata*, *ProformaInvoiceMetadata*, *XmlTorg12Metadata*, *XmlAcceptanceCertificateMetadata*, *PriceListMetadata*, *PriceListAgreementMetadata*, *CertificateRegistryMetadata*, *ReconciliationActMetadata*, *ContractMetadata*, *Torg13Metadata*, *SupplementaryAgreementMetadata*, *ServiceDetailsMetadata*, *UniversalTransferDocumentMetadata*, *UniversalTransferDocumentRevisionMetadata*, *UniversalCorrectionDocumentMetadata* и *UniversalCorrectionDocumentRevisionMetadata* теперь считаются **устаревшими** и **не рекомендованы** к использованию. В будущем они будут удалены. 


v.1.49.2 - 08.02.2018
---------------------

- Расширена структура :doc:`proto/PrepareDocumentsToSignRequest` метода :doc:`http/PrepareDocumentsToSign`: добавлена структура `ContentToPatch` для патчинга содержимого документов.
- Добавлен метод для создания сообщения с документами на основе шаблона :doc:`http/TransformTemplateToMessage`.
- Добавлена универсальная структура в MessagePatchToPost.RecipientTitles для отправки второго титула любого типа документов. Рекомендуется использовать это поле вместо XmlTorg12BuyerTitles, XmlAcceptanceCertificateBuyerTitles, UniversalTransferDocumentBuyerTitles и др.

v.1.49.1 - 09.01.2018
---------------------

- Появился параметр `count` для метода :doc:`http/GetDocuments`


v.1.49 - 21.12.2017
-------------------

Появились новые методы для работы с шаблонами документов:

- Метод для отправки шаблона документов :doc:`http/PostTemplate`.

- Метод для получения отправленного шаблона :doc:`http/GetTemplate`.

- В структуре данных Organization добавлено поле `IsForeign`, отражающее статус иностранности организации.

v.1.48 - 25.10.2017
-------------------

- Появился новый метод :doc:`http/GetDocumentTypes`, возвращающий описание типов документов, доступных в ящике.

- В структуре :doc:`proto/MessageToPost`, которую принимает метод :doc:`/V3/PostMessage <http/PostMessage>`, изменилось поле CustomDocumentAttachments. Теперь оно называется :doc:`DocumentAttachments <proto/DocumentAttachment>` и может использоваться для отправки документов любых типов.

19.10.2017
----------

- Добавили ограничение на количество документов в структуре :doc:`proto/MessageToPost`, которую можно отправить через метод :doc:`http/PostMessage`. Текущее максимально допустимое количество документов в сообщении - 30.

v.1.47.1 - 18.09.2017
---------------------
- В структуре :doc:`../proto/User`, которая возвращается методом :doc:`/GetMyUser <http/GetMyUser>`, изменилась структура CertificateInfo. В неё были добавлены два новых поля: *OrganizationName* - наименование организации, на которую выдан сертификат и *Inn* - ИНН организации, на которую выдан сертификат.


v.1.47 - 06.09.2017
---------------------
- В API Диадока появилась новая версия метода :doc:`/V4/GetMessage <http/GetMessage>`. Основное отличие версии *V4* от версии *V3* в том, что новая версия метода имеет дополнительную опцию *injectEntityContent*. Подробное описание есть метода :doc:`здесь <http/GetMessage>`.


v.1.46.2 - 31.08.2017
---------------------
- Появилась новая структура данных :doc:`CancellationInfo <proto/CancellationInfo>`, содержащая информацию об отмене сущности.

- Изменилось поведение :doc:`GetMessage <http/GetMessage>`. Возвращаются отменённые запросы на согласование вместе с соответствующими сущностями отмены. Ранее, отменённый запрос на согласование не возвращался и, соответственно, не было возможности определить, что данный запрос на соглавание был отменён.

v.1.46.1 - 30.08.2017
---------------------

- Добавили структуры :doc:`proto/TovTorgInfo` и :doc:`proto/AcceptanceCertificate552Info` для описания накладных и актов в формате приказов №551/552.


v.1.46 - 23.08.2017
---------------------
- Появилась новая структура данных :doc:`SignatureInfo <proto/SignatureInfo>`, содержащая информацию о подписи и сертификате.

- Добавлен метод :doc:`GetSignatureInfo <http/GetSignatureInfo>`, получающий на вход идентификаторы подписи и возвращающий данные в структуре :doc:`SignatureInfo <proto/SignatureInfo>`.

- В структуре данных :doc:`InvoiceItemAmountsDiff <proto/InvoiceCorrectionInfo>` поле *Subtotal*, отражающее сумму с учетом налога, теперь является опциональным.

- Появилась вторая версия метода :doc:`ExtendedSignerDetails <http/utd/ExtendedSignerDetailsV2>`, принимающая на вход структуру :doc:`DocumentTitleType <proto/DocumentTitleType>`


v.1.44.2 - 13.07.2017
---------------------

Добавлены следующие поля:

- В структуре данных :doc:`Organization <proto/Organization>` добавлено поле *CertificateOfRegistryInfo*, в котором указана информация о свидетельстве о государственной регистрации.

- В структуре данных :doc:`DocumentInfo <proto/DocumentInfo>` добавлено поле *AttachmentVersion*, в котором указана версия документа.



v.1.44.1 - 29.06.2017
---------------------

Добавлен признак "Разрешить посылать зашифрованные документы".

В структуре данных :doc:`Box <proto/Organization>` появилось поле *EncryptedDocumentsAllowed*, в котором указан признак "Разрешить посылать зашифрованные документы".



v.1.44 - 06.06.2017
---------------------

Добавлено наименование первичного документа.

В структуре данных :doc:`EncryptedXmlDocumentAttachment <proto/EncryptedXmlDocumentAttachment>` появилось поле *DocumentName*, в котором указано наименование первичного документа, определенное организацией (НаимДокОпр).



v.1.43 - 02.06.2017
---------------------

Добавлена дата ликвидации организации.

В структуре данных :doc:`Organization <proto/Organization>` появилось поле *LiquidationDate*, в котором указана дата ликвидации организации по данным из ЕГРЮЛ и ЕГРИП.



v.1.42 - 03.05.2017
---------------------

Добавлены подписи промежуточных получателей и их статусы.

В структуре данных :doc:`Document <proto/Document>` появилось поле *ProxySignatureStatus*, отвечающее за статус подписи промежуточного получателя. В структуре :doc:`Message <proto/Message>` в поле *Entities* теперь возвращаются сами подписи промежуточного получателя.



v.1.41.3 - 11.04.2017
---------------------

Появилась возможность определить версию XSD-схемы, в соответствии с которой был отправлен документ.

В структурах данных :doc:`Document <proto/Document>` и :doc:`Entity <proto/Entity message>` появилось поле *AttachmentVersion*. Значения, возвращаемые в данном поле, показывают версию XSD-схемы. Версия XSD возвращается для документов, сформированных в соответствии с приказами ФНС №155 от 24 марта 2016 и №189 от 13 апреля 2016. В дальнейшем планируется расширение перечня возвращаемых значений.



v.1.41.1 - 30.03.2017
---------------------

Появилась возможность отправлять неформализованные акты и акты сверки без указания номера документа.

В структурах данных :doc:`ReconciliationActAttachment <proto/ReconciliationActAttachment>` и :doc:`AcceptanceCertificateAttachment <proto/AcceptanceCertificateAttachment>`
поле *DocumentNumber* стало необязательным.


v1.41 - 27.03.2017
------------------

В API Диадока появилась возможность снимать документ с маршрута согласования, подробнее см. описание поля
*ResolutionRouteRemovals* в структуре :doc:`MessagePatchToPost <proto/MessagePatchToPost>`. Также произошла
замена термина "цепочка согласования" на маршрут согласования в документации, а в названиях структур данных и HTTP-методах
слово Chain было заменено словом Route.

Полный список всех переименований:

-  в enum-е :doc:`AttachmentType <proto/Entity message>` элемент *ResolutionChainAssignment* переименован в *ResolutionRouteAssignment*

-  в структуре :doc:`MessagePatchToPost <proto/MessagePatchToPost>` поле *ResolutionChainAssignments* переименовано в *ResolutionRouteAssignments*

-  структура *ResolutionChainAssignment* переименована в :doc:`ResolutionRouteAssignment <proto/MessagePatchToPost>`

-  в структуре :doc:`ResolutionRouteAssignment <proto/MessagePatchToPost>` поле *ChainId* переименовано в *RouteId*

-  структура *ResolutionChainList* переименована в :doc:`ResolutionRouteList <proto/ResolutionRoute>`

-  в структуре :doc:`ResolutionRouteList <proto/ResolutionRoute>` поле *ResolutionChains* переименовано в *ResolutionRoutes*

-  структура *ResolutionChain* переименована в :doc:`ResolutionRoute <proto/ResolutionRoute>`

-  в структуре :doc:`ResolutionRoute <proto/ResolutionRoute>` поле *ChainId* переименовано в *RouteId*

-  HTTP-метод *GetResolutionChainsForOrganization* переименован в :doc:`GetResolutionRoutesForOrganization <http/GetResolutionRoutesForOrganization>`

v1.40 - 24.03.2017
------------------

В API Диадока появились методы для парсинга титулов УКД: :doc:`продавца <http/utd/ParseUniversalCorrectionDocumentSellerTitleXml>` и :doc:`покупателя <http/utd/ParseUniversalCorrectionDocumentBuyerTitleXml>`

v1.39 - 15.03.2017
------------------

В API Диадока появилась новая версия метода :doc:`/V5/GetNewEvents /<http/GetNewEvents>`, для получения ленты событий по ящику.

Основное отличие версии *V5* от версии *V4* в том, что новая версия метода работает для всех пользователей в ящике.

Лента событий формируется по подразделению организации, в котором состоит пользователь. Подробное описание есть метода :doc:`здесь /<http/GetNewEvents>`.

v1.38.3 - 10.02.2017
--------------------

В структуре :doc:`OrganizationWithCounteragentStatus <proto/GetOrganizationsByInnListRequest>` добавилось поле *LastEventTimestampTicks*.

v1.38 - 23.12.2016
------------------

В Диадоке появилась возможность работать с новыми типами документов УПД и УКД, в связи с чем в документации появились новые разделы:

-  Добавлены новые разделы, описывающие:

    -  :doc:`документооборот счетов-фактур <docflows/InvoiceDocflow>`,

    -  :doc:`документооборот накладных <docflows/Torg12Docflow>`,

    -  :doc:`документооборот актов <docflows/AktDocflow>`,

    -  :doc:`документооборот УПД/УКД <docflows/UtdDocflow>`,

-  Добавлен раздел, описывающий методы и структуры для работы :doc:`с УПД <API_UniversalTransferDocument>`

Появились новые методы API:

-  генерация титула продавца УПД и УКД - :doc:`http/utd/GenerateUniversalTransferDocumentXmlForSeller`

-  генерация титула покупателя УПД и УКД - :doc:`http/utd/GenerateUniversalTransferDocumentXmlForBuyer`

-  парсинг титула продавца УПД - :doc:`http/utd/ParseUniversalTransferDocumentSellerTitleXml`

-  парсинг титула покупателя УПД - :doc:`http/utd/ParseUniversalTransferDocumentBuyerTitleXml`

-  заполнение дополнительных данных (для УПД и УКД) о подписантах  - :doc:`http/utd/ExtendedSignerDetailsV2`

Появились новые структуры в API:

-  структура для описания титула продавца УПД - :doc:`proto/utd/UniversalTransferDocumentSellerTitleInfo`

-  структура для описания титула покупателя УПД - :doc:`proto/utd/UniversalTransferDocumentBuyerTitleInfo`

-  структура для описания титула продавца УКД - :doc:`proto/utd/UniversalCorrectionDocumentSellerTitleInfo`

-  структура для описания титула покупателя УКД - :doc:`proto/utd/UniversalTransferDocumentBuyerTitleInfo`

-  структура для описания данных УПД и УКД - :doc:`proto/utd/UniversalDocumentMetadata`

-  структура для описания реквизитов продавца, покупателя и грузоотправителя, используемая в УПД и УКД - :doc:`proto/utd/ExtendedOrganizationInfo`

-  структура для описания реквизитов подписанта, используемая в УПД и УКД - :doc:`proto/utd/ExtendedSigner`

-  структура для описания реквизитов подписанта, используемая в методе :doc:`proto/utd/ExtendedOrganizationInfo` - :doc:`proto/utd/ExtendedSignerDetailsToPost`

В структуре :doc:`proto/MessageToPost` добавилось поле *UniversalTransferDocumentSellerTitles*:

-  для отправки УПД с функцией СЧФ,

-  для отправки УКД с функцией КСЧФ,

-  для отправки титула продавца УПД с функцией ДОП и СЧФДОП,

-  для отправки титула продавца УКД с функцией ДОП и СЧФДОП,

Для отправки титула покупателя УПД и УКД в структуре :doc:`proto/MessageToPost` добавилось поле *UniversalTransferDocumentBuyerTitles*:

-  для отправки титула покупателя УПД с функцией ДОП и СЧФДОП,

-  для отправки титула покупателя УКД с функцией ДОП и СЧФДОП,

В структуру :doc:`proto/PrepareDocumentsToSignRequest` добавилась возможность указать расширенные данные о подписанте.

В DocflowAPI произошли следующие изменения:

-  добавились новые структуры для описания документооборота УПД:

    -  входящий УПД - :doc:`proto/utd/docflow/InboundUniversalTransferDocumentDocflow`

    -  исходящий УПД - :doc:`proto/utd/docflow/OutboundUniversalTransferDocumentDocflow`

    -  дополнительные данные о УПД - :doc:`proto/utd/docflow/UniversalTransferDocumentInfo`

    -  дополнительные данные о УКД - :doc:`proto/utd/docflow/UniversalCorrectionDocumentInfo`

-  в структуру :doc:`proto/Docflow` добавились поля *InboundUniversalTransferDocumentDocflow* и *OutboundUniversalTransferDocumentDocflow*

-  в структуру :doc:`proto/DocumentInfo` добавились поля *UniversalTransferDocumentInfo* и *UniversalCorrectionDocumentInfo*.


v1.37 - 10.10.2016
------------------

Добавлена структура для отправки кастомных типов документов - :doc:`CustomDocumentAttachment <proto/DocumentAttachment>`.

.. note::
    Функциональность находится в разработке


v1.36 - 07.04.2016
------------------

- Добавлен параметр *includeRelations* у метода :doc:`http/GetOrganizationsByInnKpp`, который позволяет получить данные о количестве запросов на поиск и приглашения к сотрудничеству для данной организации.

v1.35 - 25.03.2016
------------------

- Добавлена возможность авторизации по логину/паролю и сертификату с ключом, полученным доверенным сервисом (см. описание методов :doc:`http/Authenticate` и :doc:`http/AuthenticateConfirm`)

v1.34 - 10.03.2016
------------------

- Добавлена возможность редактировать пакеты документов:

    - В структуре :doc:`proto/MessagePatchToPost` добавлено поле EditDocumentPacketCommands.

    - Добавлена новая структура :doc:`EditDocumentPacketCommand <proto/MessageToPost>`, описывающая операцию редактирования пакета документов.

v1.33 - 10.02.2016
------------------

- Добавлен метод :doc:`http/GetDepartment`, позволяющий получить информацию о конкретном подразделении организации.

v1.32 - 19.01.2016
------------------

- Значения перечисления ResolutionType (:doc:`proto/Resolution`) синхронизированы со значениями, возвращаемые с сервера (значение Undefined заменено на UndefinedResolutionType)
- В структуру :doc:`proto/MessageToPost` добавлен флаг залоченного пакета *LockPacket*.

v1.31 - 02.12.2015
------------------

-  Добавлено свойство с сообщением об ошибке при доставке в роуминг *RoamingNotificationStatusDescription* в структуре :doc:`proto/Document`.

-  Добавлены новые версии методов :doc:`http/GetCounteragent` и :doc:`http/GetCounteragents`, в которых изменилась логика показа видимых подразделений.

v1.30 - 11.11.2015
------------------

-  Добавлено свойство признак прочитанности *IsRead* в структуре :doc:`proto/Document`.
-  В методе :doc:`http/GetDocuments` теперь можно искать непрочитанные документы.


v1.29 - 14.10.2015
------------------

-  Появилась возможность отправлять новый тип документа "Дополнительное соглашение к договору".

    -  в структуре :doc:`proto/MessageToPost` добавилась стуктура :doc:`proto/SupplementaryAgreementAttachment` для передачи дополнительного соглашения к договору

    -  в структуре :doc:`proto/Entity message` и :doc:`proto/DocumentType` появился новый тип для дополнительного соглашения к договору

    -  в структуре :doc:`proto/Document` появилась вложенная структура для описания метаданных дополнительного соглашения к договору - :doc:`SupplementaryAgreementMetadata <proto/BilateralDocumentMetadata>`

    -  в структуре :doc:`proto/DocumentInfo` появилась вложенная структура для описания метаданных дополнительного соглашения к договору - :doc:`SupplementaryAgreementInfo <proto/SupplementaryAgreementDocumentInfo>`



v1.28 - 10.08.2015
------------------

-  Добавилась возможность отправлять зашифрованные товарные накладные и акты выполненных работ. Для этого были внесены следующие изменения:

    -  в структуре :doc:`proto/MessageToPost` добавились поля *EncryptedXmlTorg12SellerTitles*, *EncryptedXmlAcceptanceCertificateSellerTitles*

    -  появилась структура :doc:`proto/EncryptedXmlDocumentAttachment` для передачи зашифрованных накладных и актов


v1.27 - 10.08.2015
------------------

-  Добавлен параметр *autoRegister* у метода :doc:`http/GetMyOrganizations`, который позволяет управлять автоматической регистрацией пользователя с сертификатом КЭП в организации.

v1.26 - 30.07.2015
------------------

-  Добавилась возможность отправлять зашифрованные счета-фактуры. Для этого были внесены следующие изменения:

    -  появились структуры :doc:`CounteragentCertificateList <proto/Counteragent>` и :doc:`Certificate <proto/Counteragent>` для описания списка сертификатов контрагента

    -  в структурах :doc:`proto/Document` и :doc:`proto/Entity message` появился флаг *IsEncryptedContent*, этот флаг указывается для передачи контента в зашифрованном виде

    -  появились структуры :doc:`proto/EncryptedInvoiceAttachment`, :doc:`EncryptedDocumentMetadata <proto/EncryptedInvoiceAttachment>`, :doc:`EncryptedInvoiceMetadata <proto/EncryptedInvoiceAttachment>`, :doc:`EncryptedInvoiceCorrectionMetadata <proto/EncryptedInvoiceAttachment>` для передачи зашифрованных счетов-фактур, и метаданных для исправлений и корректировок.

    -  в структуре :doc:`proto/MessageToPost` добавилось поле *EncryptedInvoices*, для передачи зашифрованных счетов-фактур

    -  в структуре :doc:`proto/MessagePatchToPost` добавилось поле *SignatureVerifications*, для передачи резльтатов проверки подписей на стороне получателя

    -  появился метод :doc:`http/GetCounteragentCertificates` для запроса списка сертификатов контрагента

    -  в структуре :doc:`proto/Signer` добавилося отпечаток сертификата *SignerCertificateThumbprint*

-  Добавилась возможность изменения подписанта в неотправленных исходящих документах:

    -  появилась структура :doc:`DocumentToPatch <proto/PrepareDocumentsToSignRequest>` представляющая изменение исходящего неотправленного документа

    -  изменились структуры :doc:`proto/DocumentSignature`, :doc:`proto/PrepareDocumentsToSignRequest` - в них добавилась возможность ссылаться на изменение исходящего неотправленного документа

v1.25 - 28.05.2015
------------------

-   Добавлен новый метод :doc:`http/GetResolutionRoutesForOrganization` для получения списка цепочек согласования организации. Также изменен протобуфер :doc:`proto/MessagePatchToPost` -  добавились структура *ResolutionChainAssignment* для постановки документа на цепочку согласования.

v1.24 - 25.05.2015
------------------

-   Добавлен новый метод для получения печатной формы со штампом для пересланного документа - :doc:`http/GenerateForwardedDocumentPrintForm`

v1.23 - 28.04.2015
------------------

-  Добавлен метод аутентификации по ключу, полученному доверенным сервисом (см. описание метода :doc:`http/Authenticate`)

v1.22.1 - 13.04.2015
--------------------

-  Изменены структуры данных :doc:`proto/InvoiceInfo` и :doc:`proto/InvoiceCorrectionInfo`, которые предоставляют исходные данные для формирования СФ и КСФ в XML-формате при помощи метода :doc:`http/GenerateInvoiceXml`

-  Появилась возможность указывать версию формата СФ и КСФ и также указывать поля, соответствующие новой версии XML-формата СФ

-  Изменилась логика работы метода :doc:`http/ParseInvoiceXml` в зависимости от формата СФ

-  Версия сборки SDK не изменилась, **всем кто скачал сборку в период с *10.04.2015-12.04.2015*, необходимо скачать свежую сборку от 13.04.2015**

v1.22 - 10.04.2015
------------------

-  Изменены структуры данных :doc:`proto/InvoiceInfo` и :doc:`proto/InvoiceCorrectionInfo`, которые предоставляют исходные данные для формирования СФ и КСФ в XML-формате при помощи метода :doc:`http/GenerateInvoiceXml`, появилась возможность указывать версию формата СФ и КСФ.

v1.21 - 02.04.2015
------------------

-  Добавлена возможность отравлять приглашения организациям, не подключенным к Диадоку. Соответствующие изменения были внесены в методы :doc:`http/AcquireCounteragent` и :doc:`http/AcquireCounteragentResult`.

Старая версия метода :doc:`http/AcquireCounteragent` через некоторое время будет отключена.

v1.20 - 20.01.2015
------------------

-  Добавлены методы для работы с :doc:`облачной ЭП <CloudSignApi>`

v1.19 - 15.10.2014
------------------

-  Добавлен метод :doc:`http/GenerateDocumentZip`, позволяющий формировать zip-архив с документом, подписями к нему и файлами документооборота.

v1.18 - 02.10.2014
------------------

-  Добавлена возможность привязывать к документам произвольные данные "ключ-значение". Соответствующие изменения были внесены в структуры :doc:`proto/MessageToPost` и :doc:`proto/MessagePatchToPost`.

v1.17 - 05.06.2014
------------------

-  В Диадоке появилась возможность получать статус доставки документа в роуминг - :doc:`proto/RoamingNotification`

v1.16 - 25.02.2014
------------------

В Диадоке появилась поддержка новых типов полуформализованных документов:

-  :doc:`протоколов согласования цены <proto/NonformalizedAttachment>`,
-  :doc:`реестров сертификатов <proto/NonformalizedAttachment>`,
-  :doc:`актов сверки <proto/ReconciliationActAttachment>`,
-  :doc:`договоров <proto/ContractAttachment>`,
-  :doc:`детализаций <proto/ServiceDetailsAttachment>`
-  :doc:`накладных ТОРГ-13 <proto/Torg13Attachment>`.

v1.15 - 05.02.2014
------------------

-  Появилась возможность получать через API протокол передачи документа. См. описание метода :doc:`http/GenerateDocumentProtocol`.

Выгрузка протокола передачи документа адресатом пересылки документа третьей стороне производится при помощи метода :doc:`http/GenerateForwardedDocumentProtocol`.

v1.14 - 24.01.2014
------------------

-  Появилась возможность пересылать документы третьей стороне. См. описание методов :doc:`http/ForwardDocument`, :doc:`http/GetForwardedDocuments` и :doc:`http/GetForwardedDocumentEvents`.

Выгрузка содержимого связанных с документом сущностей адресатом пересылки документа третьей стороне производится при помощи метода :doc:`http/GetForwardedEntityContent`.

v1.11 - 20.12.2013
------------------

-  Сборка protobuf-net.dll теперь внедрена в библиотеку DiadocApi.dll. Это позволяет интегратору использовать в своем проекте другую версию сборки protobuf-net.dll.

v1.10 - 06.12.2013
------------------

-  В Диадоке появилась возможность отправлять формализованные отказы от подписи документов. Xml файл отказа формируется при помощи метода :doc:`http/GenerateSignatureRejectionXml`.

    Для отправки отказов используется метод :doc:`http/PostMessagePatch`, куда передается структура :doc:`proto/MessagePatchToPost` с заполненным списком :doc:`MessagePatchToPost.XmlSignatureRejections <proto/MessagePatchToPost>`.

Для получения документов с отказом в подписи через метод :doc:`http/GetDocuments` используются такие же фильтры, как для неформализованных отказов. Формализованным отказам соответствует тип XmlSignatureRejection из перечисления :doc:`AttachmentType <proto/Entity message>`.

-  Отправка неформализованных отказов от подписи в адрес роуминговых организаций теперь запрещена.

-  Новые отказы от подписи, при получении их через старые версии SDK, будут иметь тип :doc:`SignatureRequestRejection <proto/Entity message>` (как отказы старого формата), но в содержимом соответствующих сущностей вместо строки с комментарием к отказу теперь будет возвращаться xml файл отказа в кодировке CP1251.

v1.9 - 20.10.2013
-----------------

-  В Диадоке появилась возможность аннулирования документов.

Для отправки предложения об аннулировании через API при обращении к методу :doc:`http/PostMessagePatch` следует наполнять список :doc:`MessagePatchToPost.RevocationRequests <proto/MessagePatchToPost>`.

Каждый элемент этого списка представляет собой структуру :doc:`RevocationRequestAttachment <proto/MessagePatchToPost>`.

Для принятия предложения об аннулировании через API при обращению к методу :doc:`http/PostMessagePatch` следует наполнять список :doc:`MessagePatchToPost.RequestedSignatures <proto/MessagePatchToPost>`.

Для отказа от предложения об аннулировании через API при обращении к методу :doc:`http/PostMessagePatch` следует наполнять список :doc:`MessagePatchToPost.XmlSignatureRejections <proto/MessagePatchToPost>`.

Каждый элемент этого списка представляет собой структуру :doc:`XmlSignatureRejectionAttachment <proto/MessagePatchToPost>`. При получение информации о документах через API при помощи методов :doc:`http/GetMessage`, :doc:`http/GetDocument` и т.п. для любых документов в структуре :doc:`proto/Document` заполняется поле :doc:`RevocationStatus <proto/Document>`.

-  Добавлены методы :doc:`http/GenerateRevocationRequestXml` и :doc:`http/GenerateSignatureRejectionXml`, облегчающие процесс формирования корректных XML файлов предложения об аннулировании и формализованного отказа в подписи.

-  Добавлены методы :doc:`http/ParseRevocationRequestXml` и :doc:`http/ParseSignatureRejectionXml`, позволяющие преобразовывать xml-файлы предложения об аннулировании и формализованного отказа в подписи в структуры :doc:`proto/RevocationRequestInfo` и :doc:`proto/SignatureRejectionInfo` соответственно.

v1.8 - 13.08.2013
-----------------

-  Произошли изменения в API по работе со списками контрагентов. См. описание методов :doc:`http/GetCounteragents`, :doc:`http/AcquireCounteragent` и :doc:`http/BreakWithCounteragent`.

v1.7 - 10.04.2013
-----------------

-  В Диадоке появилась поддержка нового типа полуформализованных документов - ценовых листов.

Ценовой лист представляет собой двусторонний документ (для него требуется подпись контрагента / отказ в запросе подписи) со следующими обязательными реквизитами: дата составления и номер самого ценового листа, дата вступления ценового листа в силу, дата и номер договора, к которому относится ценовой лист.

Для отправки ценовых листов через API при обращении к методу :doc:`http/PostMessage` следует наполнять список :doc:`MessageToPost.PriceLists <proto/MessageToPost>`.

Каждый элемент этого списка представляет собой структуру :doc:`proto/PriceListAttachment`.

При получение информации о документах через API при помощи методов :doc:`http/GetMessage`, :doc:`http/GetDocument` и т.п. для ценовых листов в структуре :doc:`proto/Document` заполняется поле :doc:`PriceListMetadata <proto/BilateralDocumentMetadata>`.

При фильтрации документов методом :doc:`http/GetDocuments` также можно использовать новый тип документов PriceList.

-  Для получения списка пользователей конкретной организации добавлен метод :doc:`http/GetOrganizationUsers`.

-  У структуры :doc:`proto/Organization` добавлено поле IfnsCode, позволяющее получить код налоговой инспекции - место подачи декларации по НДС.

v1.6 - 14.03.2013
-----------------

-  Добавлена возможность отправлять документы, подписанные тестовой подписью (см. описание флага :doc:`SignedContent.SignWithTestSignature <proto/SignedContent>`).

-  Добавлены методы :doc:`http/ParseAcceptanceCertificateSellerTitleXml` и :doc:`http/ParseTorg12SellerTitleXml`, позволяющие преобразовывать xml-файлы формализованных актов (титул исполнителя) и ТОРГ-12 (титул продавца) в структуры :doc:`AcceptanceCertificateSellerTitleInfo <proto/AcceptanceCertificateInfo>` и :doc:`Torg12SellerTitleInfo <proto/Torg12Info>` соответственно.

-  Функциональность метода :doc:`http/PostMessage` была расширена: при помощи флага :doc:`MessageToPost.DelaySend <proto/MessageToPost>` можно задержать отправку документа, чтобы была возможность провести его согласование. В связи с этим изменился набор возможных состояний документов, что требует обновления логики клиентских решений.

-  Для определения, может ли конкретный пользователь запрашивать согласования, может использоваться флаг :doc:`OrganizationUserPermissions.CanRequestResolutions <proto/OrganizationUserPermissions>` в свойствах пользователя, :doc:`возвращаемых вызовом GetMyPermissions <http/GetMyPermissions>`.

-  В сообщение :doc:`EntityPatch <proto/MessagePatch>` добавлено поле ContentIsPatched, через которое сервер выдает информацию о том, что исходный документ в процессе подписания был модифицирован (в документ была внедрена информация о том, кто подписал этот документ).

-  Изменена логика работы с перечислимыми типами: теперь в большинстве перечислений имеется специальное значение с именем UnknownИмяПеречисления.

Клиент может получить (и получит) такое значение в том и только том случае, если имеет место рассогласование версий API между клиентом и сервером, и клиент не может правильно интерпретировать информацию, возвращаемую сервером (например, в случае добавления новых элементов к перечислению клиент будет получать вместо вновь добавленных элементов этот самый UnknownИмяПеречисления элемент). Клиент обязан корректно обрабатывать такие ситуации (например, путем информирования пользователя о необходимости обновить интеграционный модуль).

Для доступа к новой функциональности и во избежание возможного конфликта версий убедительная просьба скачать и обновить версию инструментария для разработчиков `Diadoc SDK v1.6 <https://diadoc.kontur.ru/sdk/>__`

v1.5 - 31.01.2013
-----------------

-  Появилась возможность работы с документами, пересылаемыми внутри организации.

Для этого добавились новые элементы в перечислениях :doc:`NonformalizedDocumentStatus <proto/NonformalizedDocumentMetadata>`, :doc:`BilateralDocumentStatus <proto/BilateralDocumentMetadata>` и :doc:`UnilateralDocumentStatus <proto/UnilateralDocumentMetadata>`, а также добавились поля для работы с подразделениями организации в структурах :doc:`proto/Department`, :doc:`Entity <proto/Entity message>`, :doc:`proto/Document`, :doc:`proto/Message` и :doc:`proto//MessageToPost`.

-  Были расширены возможности работы с «черновиками», то есть с подготовленными, но не отправленными документами. Для отправки ранее созданного черновика добавился метод :doc:`http/SendDraft`.

Кроме того, черновики теперь можно загружать в Диадок при помощи метода :doc:`http/PostMessage` (это предпочтительный путь).

Для этого обновилась структура :doc:`proto//MessageToPost`, добавилась структура :doc:`proto/DraftToSend` и структура RequestedSignature была переименована в DocumentSignature (см. описание :doc:`proto/MessagePatchToPost`).

-  Появилась возможность загружать большие по размеру документы в Диадок при помощи сервиса «полки документов». Для этих целей добавился метод :doc:`http/ShelfUpload` и обновилась структура :doc:`proto/SignedContent`, в которой появилось поле NameOnShelf, позволяющее сослаться на уже загруженный на «полку» файл.

-  Появилась возможность восстанавливать ранее удаленные отдельные документы и сообщения целиком. Для этих целей добавлен метод :doc:`http/Restore`, а в структурах :doc:`EntityPatch <proto/MessagePatch>` и :doc:`proto/MessagePatch` добавлены поля, позволяющие узнать, были ли конкретный документ или сообщение восстановлены.

-  Появилась возможность по документу (`Document <Document>`) или сообщению (`Message <Message>`) понять, является ли он юридически значимым. Для этих целей в каждую из названных структур добавлено поле IsTest.

-  Добавилась возможность проводить эвристический семантический разбор строк, представляющих почтовый адрес в Российской Федерации. За это отвечает метод :doc:`http/ParseRussianAddress`.

-  Добавилась возможность выполнять трансформацию XML-файла СФ/ИСФ, сформированного в соответствии с :download:`XML-схемой <xsd/ON_SFAKT_1_897_01_05_01_02.xsd>`, в структуру :doc:`proto/InvoiceInfo`. За это отвечает метод :doc:`http/ParseInvoiceXml`.

v1.4 - 29.08.2012
-----------------

-  В структуру данных :doc:`proto/Organization` добавилось поле Departments, содержащее список всех подразделений в организации. Это поле позволяет получать информацию об оргструктуре при помощи методов :doc:`http/GetMyOrganizations`, :doc:`http/GetOrganization`, :doc:`http/GetCounteragents`, :doc:`http/GetCounteragent`.

-  В методах :doc:`http/PostMessage` и PostDraft появилась возможность отправлять документы в конкретное подразделение контрагента. Для этого в структуру данных :doc:`proto/MessageToPost` добавилось новое поле ToDepartmentId, а в метод PostDraft был добавлен новый параметр toDepartmentId.

-  Появился новый метод :doc:`http/MoveDocuments` для перемещения документов своей организации между подразделениями. Информация о перемещениях документов между подразделениями (неважно было это сделано через API или через Web) доступна через метод :doc:`http/GetNewEvents`, в структуре данных :doc:`EntityPatch <proto/MessagePatch>` добавилось поле MovedToDepartmentId.

-  В структуру данных :doc:`Entity <proto/Entity message>` добавилось поле RawCreationDate, содержащее :doc:`метку времени <proto/Timestamp>` создания сущности. Это поле заполняется для всех сущностей, его можно использовать для получения времени подписания или согласования документа.

-  Появилась возможность осуществлять согласование (или отказ в согласовании) документов через API. Для этого добавилась структура данных :doc:`proto/Resolution`, а в структуре данных :doc:`proto/MessagePatchToPost` добавилось поле Resolutions.

Все действия по согласованию видны в структуре данных :doc:`proto/Message` как сущности с типом :doc:`Attachment/Resolution <proto/Entity message>`.

Содержимое этой сущности - байты строки комментария к согласованию в кодировке UTF-8. В структуру данных :doc:`Entity <proto/Entity message>` добавилось поле  ResolutionInfo, содержащее тип действия по согласованию и ФИО согласователя в виде новой структуры данных :doc:`ResolutionInfo <proto/Resolution>`.

v1.3 - 26.06.2012
-----------------

-  Был добавлен метод :doc:`http/Delete`, позволяющий помечать документы как удаленные. Также в структурах данных :doc:`proto/Document` и :doc:`proto/Message` появились соответствующие флаги IsDeleted.

Кроме того, в структуру данных :doc:`proto/MessagePatch` был добавлен флаг MessageIsDeleted и поле EntityPatches, содержащее список структур данных типа EntityPatch с флагом DocumentIsDeleted. Данные расширения структуры данных MessagePatch позволяют отслеживать моменты удаления документов и/или сообщений, анализируя поток событий в ящике, возвращаемый методом :doc:`http/GetNewEvents`.

-  Был добавлен метод :doc:`http/CanSendInvoice`, позволяющий для данного идентификатора ящика и сертификата ЭП узнать, был ли этот сертификат зарегистрирован в ФНС в качестве сертификата, используемого для подписания электронных счетов-фактур, отправляемых участником ЭДО, которому принадлежит данный ящик в Диадоке. Проще говоря, метод CanSendInvoice отвечает на вопрос, может ли тот или иной сертификат ЭП использоваться для подписания ЭСФ, отправляемых из данного ящика. Также в структуру данных :doc:`proto/Organization` было добавлено поле FnsRegistrationDate - дата подачи заявления в ФНС на регистрацию данной организации в качестве участника документооборота ЭСФ.

-  Метод PostDraft теперь позволяет загружать в черновики товарные накладные и акты о выполнении работ / оказании услуг в рекомендованном ФНС XML-формате (документы с типами :doc:`Attachment/XmlTorg12 <proto/Entity message>` и :doc:`Attachment/XmlAcceptanceCertificate <proto/Entity message>`). Также в метод PostDraft была добавлена поддержка счетов на оплату (документов типа :doc:`Attachment/ProformaInvoice <proto/Entity message>`).

v1.2 - 09.06.2012

-  Был расширен перечень сведений, возвращаемых методами, дающими доступ к справочнику организаций в Диадоке (например, :doc:`http/GetMyOrganizations`). Теперь структура данных :doc:`proto/Organization` включает поля Ogrn (ОГРН организации), Address (юридический адрес организации) и FnsParticipantId (уникальный идентификатор участника документооборота СФ, который должен указываться при формировании XML счетов-фактур).

-  Метод :doc:`http/GenerateInvoiceXml` теперь позволяет формировать не только XML-файлы счетов-фактур, но и XML-файлы исправлений счетов-фактур, корректировочных счетов-фактур, а также исправлений корректировочных счетов-фактур.

v1.1 - 11.05.2012

-  Появилась поддержка рекомендованных ФНС России форматов электронных товарных накладных и актов о выполнении работ / оказании услуг. Теперь при помощи метода :doc:`http/PostMessage` можно загружать в Диадок титулы продавца XML-накладных (новый тип документов :doc:`Attachment/XmlTorg12 <proto/Entity message>`) и титулы исполнителя XML-актов (новый тип документов :doc:`Attachment/XmlAcceptanceCertificate <proto/Entity message>`), а при помощи метода :doc:`http/PostMessagePatch` можно загружать в Диадок соответствующие титулы покупателя/заказчика. В Diadoc SDK включены XML-схемы, описывающие рекомендованные ФНС России форматы товарных накладных и актов о выполнении работ / оказании услуг:

 -  :download:`XML-схема товарной накладной, титул продавца <xsd/DP_OTORG12_1_986_00_05_01_02.xsd>`;

 -  :download:`XML-схема товарной накладной, титул покупателя <xsd/DP_PTORG12_1_989_00_05_01_02.xsd>`;


 -  :download:`XML-схема акта о выполнении работ / оказании услуг, титул исполнителя <xsd/DP_IAKTPRM_1_987_00_05_01_02.xsd>`;

 -  :download:`XML-схема акта о выполнении работ / оказании услуг, титул заказчика <xsd/DP_ZAKTPRM_1_990_00_05_01_02.xsd>`.

 Также появились методы :doc:`http/GenerateTorg12XmlForSeller`, :doc:`http/GenerateTorg12XmlForBuyer` и :doc:`http/GenerateAcceptanceCertificateXmlForSeller` и :doc:`http/GenerateAcceptanceCertificateXmlForBuyer`, облегчающие процесс формирования корректных XML-файлов товарных накладных и актов. Поддержка новых типов документов была добавлена и в метод :doc:`http/GetDocuments`.

-  Появилась возможность при помощи метода :doc:`http/PostMessage` загружать в Диадок счета на оплату (новый тип документов :doc:`Attachment/ProformaInvoice <proto/Entity message>`). Поддержка данного типа документов была добавлена и в метод :doc:`http/GetDocuments`.

-  Также в метод :doc:`http/PostMessage` была добавлена возможность загружать в Диадок вложения специального типа "структурированные данные" (`Attachment/StructuredData <proto/Entity message>`), при помощи которого можно организовать передачу рядом с юридически-значимой печатной формой документа каких-то данных, подлежащих автоматизированной обработке.

-  Метод :doc:`http/GetDocuments` теперь позволяет получать информацию обо всех СФ-подобных документах (СФ/ИСФ/КСФ/ИКСФ) единым списком. Для этого в качестве первой части параметра filterCategory нужно передать специальное значение "AnyInvoiceDocumentType". Например, чтобы получить список всех входящих СФ/ИСФ/КСФ/ИКСФ, нужно в метод GetDocuments передать параметр filterCategory=AnyInvoiceDocumentType.Inbound.

v1.0 - 04.04.2012
-----------------

-  Появилась поддержка официально утвержденных версий форматов документов, фигурирующих в документообороте счетов-фактур. В связи с этим поменялись сигнатуры методов :doc:`http/GenerateInvoiceDocumentReceiptXml` и :doc:`http/GenerateInvoiceCorrectionRequestXml`. В Diadoc SDK включены соответствующие XML-схемы, описывающие форматы документов, фигурирующих в документообороте счетов-фактур:

 -  :download:`XML-схема счета-фактуры  (СФ) <xsd/ON_SFAKT_1_897_01_05_01_02.xsd>`;  эта же схема описывает формат исправления СФ (ИСФ);

 -  :download:`XML-схема корректировочного счета-фактуры  (КСФ) <xsd/ON_KORSFAKT_1_911_01_05_01_02.xsd>`;  эта же схема описывает формат исправления КСФ (ИКСФ);

 -  :download:`XML-схема извещения о получении  документа <xsd/DP_IZVPOL_1_982_00_01_01_02.xsd>`;

 -  :download:`XML-схема подтверждения оператора о дате отправки  СФ/ИСФ/КСФ/ИКСФ <xsd/DP_PDPOL_1_984_00_01_01_02.xsd>`  (выдается продавцу);

 -  :download:`XML-схема подтверждения оператора о дате доставки СФ/ИСФ/КСФ/ИКСФ <xsd/DP_PDOTPR_1_983_00_01_01_02.xsd>`  (выдается покупателю);

 -  :download:`XML-схема уведомления об уточнении СФ/ИСФ/КСФ/ИКСФ <xsd/DP_UVUTOCH_1_985_00_01_01_02.xsd>`  (формируется покупателем).

В целях обеспечения обратной совместимости с существующими пилотными проектами по итеграции Диадок в течение еще какого-то времени будет продолжать принимать счета-фактуры в старом формате. Однако нужно иметь в виду, что такие документы не будут иметь юридической значимости.

-  Появился метод :doc:`http/GenerateInvoiceXml`, облегчающий процесс формирования корректного XML-файла счета-фактуры.

Данный метод позволяет интегратору не погружаться в детали XML-формата СФ, а передавать в Диадок только необходимые первичные данные в виде структуры :doc:`proto/InvoiceInfo`. По этим данным метод GenerateInvoiceXml, при необходимости дополнив их сведениями из своих справочников, сформирует корректный XML-файл счета-фактуры, который затем можно будет отправить методом :doc:`http/PostMessage`, либо загрузить в черновики методом PostDraft. В частности, в структуре InvoiceInfo можно вообще не заполнять реквизиты продавца и покупателя, достаточно указать идентификаторы их ящиков в Диадоке, и тогда соответствующие реквизиты будут подтянуты из справочника организаций Диадока.

-  В Диадоке появилась возможность работать с исправлениями счетов-фактур и корректировочными счетами-фактурами. Для этого были введены новые :doc:`типы сущностей <proto/Entity message>`: Attachment/InvoiceRevision (исправление счета-фактуры), Attachment/InvoiceCorrection (корректировочный счет-фактура), Attachment/InvoiceCorrectionRevision (исправление корректировочного счета-фактуры). Для связывания исправлений и корректировок с оригинальными СФ нужно использовать уже имеющийся в Диадоке механизм установки ссылок между документами, находящимися в разных сообщениях. Кроме того, в структуре :doc:`Document.InvoiceMetadata <proto/InvoiceDocumentMetadata>`, описывающей метаданные счета-фактуры в Диадоке, появилось поле InvoiceAmendmentFlags, которое отражает статус счета-фактуры с точки зрения наличия уведомления об уточнении или отправленного исправления / корректировки. Например, при отправке корректировочного СФ, у исходного счета-фактуры, по которому было запрошено уточнение, поле Document.InvoiceMetadata.InvoiceAmendmentFlags поменяет свое значение с AmendmentRequested на AmendmentRequested\|Corrected.

-  Появился метод :doc:`http/GetInvoiceCorrectionRequestInfo`, позволяющий получить информацию, содержащуюся в уведомлении об уточнении счета-фактуры, без необходимости уметь разбирать соответствующий XML-формат, утвержденный ФНС, что в какой-то степени упрощает работу интегратора. В частности, метод GetInvoiceCorrectionRequestInfo позволяет получить текст уведомления об уточнении.

-  Появилась возможность при помощи методов :doc:`http/PostMessage` и PostDraft загружать в Диадок акты о выполнении работ / оказании услуг (новый тип документов :doc:`Attachment/AcceptanceCertificate <proto/Entity message>`). Поддержка нового типа документов была добавлена и в метод :doc:`http/GetDocuments`.

-  Метод :doc:`http/GetDocuments` научился фильтровать список документов по дате формирования документа в учетной системе (реквизиту самого документа), а не только по дате загрузки документа в Диадок. Для этого в метод GetDocuments добавлены необязательные параметры строки запроса fromDocumentDate и toDocumentDate, которые позволяют задать интервал времени, в котором осуществляется поиск. При этом метод GetDocuments продолжает поддерживать фильтрацию списка документов при помощи параметров timestampFromTicks и timestampToTicks.

-  Было расширено API для работы с черновиками:

    -  Метод :doc:`http/GetNewEvents` теперь возвращает  информацию  о событиях, происходящик с черновиками: создание черновика (и  начальный набор документов в нем), добавление к черновику  документов, утилизация черновика (просто удаление, либо отправка  на основе него полноценного сообщения). Методы  :doc:`http/GetEvent` и :doc:`http/GetMessage` также  теперь  возвращают информацию о черновиках.

 -  Появился метод :doc:`http/RecycleDraft`, который  позволяет  удалять еще не отправленные черновики.

 -  У сообщения :doc:`proto/Message` появилось необязательное поле  CreatedFromDraftId, в которое заносится идентификатор черновика,  на основании которого было создано данное сообщение (или  черновик). Также и у черновика появилось симметричное поле  DraftIsTransformedToMessageId, куда заносится идентификатор  сообщения (или черновика), которое было создано из данного  черновика. Флаг Message.DraftIsRecycled означает, что черновик  был утилизирован, то есть просто удален, либо преобразован в  полноценное сообщение или в другой черновик. Соответственно,  поля DraftIsTransformedToMessageId и DraftIsRecycled могут  присутствовать в структуре Message, описывающей черновик,  одновременно.
 -  Метод PostDraft стал позволять создавать нередактируемые  черновики, то есть такие черновики, которые можно только  отправить, или удалить. Добавление или удаление документов из  таких черновиком заблокировано как в веб-интерфейсе Диадока, так  и в API-методе PostDraft. Для создания нередактируемого  черновика нужно в метод PostDraft передать параметр lock без  значения.

v0.9 - 18.01.2012
-----------------

-  Появились методы для управления списком своих контрагентов. Метод :doc:`http/GetCounteragents` позволяет получить список контрагентов, отфильтрованный по их статусу. Метод :doc:`http/GetCounteragent` позволяет получить информацию о контрагенте по его идентификатору. Метод :doc:`http/AcquireCounteragent` позволяет добавить организацию в список своих контрагентов. Метод :doc:`http/BreakWithCounteragent` позволяет исключить организацию из списка своих контрагентов.

-  Был переработан механизм получения справочной информации об организациях и ящиках в Диадоке. Методы GetBoxInfo и GetBoxesByInnKpp, а также метод GetBoxesByAuthToken объявлены устаревшими и не рекомендуются к использованию. Через некоторое время их поддержка будет прекращена. Вместо метода GetBoxesByAuthToken теперь нужно использовать метод :doc:`http/GetMyOrganizations`, позволяющий получить информацию обо всех организациях и ящиках, к которым имеет доступ владелец текущего авторизационного токена. Вместо метода GetBoxesByInnKpp теперь нужно использовать метод :doc:`http/GetOrganizationsByInnKpp`, позволяющий получить информацию о ящиках в Диадоке по ИНН и КПП организации. Наконец, на смену методу GetBoxInfo пришли методы :doc:`http/GetOrganization` и :doc:`http/GetBox`, позволяющие получить информацию соответственно о конкретных организации и ящике по их идентификаторам.

v0.8 - 16.12.2011
-----------------

-  Появился метод :doc:`http/GetDocuments`, позволяющий быстро получать информацию о документах (например, о счетах-фактурах) в своем ящике, задавая различные критерии фильтрации документов. Также появился метод :doc:`http/GetDocument`, позволяющий получить всю метаинформацию об отдельном документе, зная его идентификатор.

-  Появилась возможность при помощи методов :doc:`http/PostMessage` и PostDraft загружать в Диадок новые типы докуметов, в частности, товарные накладные (ТОРГ-12) и запросы на инициацию канала обмена документами через Диадок :doc:`TrustConnectionRequest <proto/TrustConnectionRequestAttachment>`.

-  Структура данных :doc:`Entity <proto/Entity message>` расширена полем DocumentInfo. Для сущности типа Attachment это поле содержит дополнительную информацию о документе, представляемом этой сущностью.

v0.7 - 03.10.2011
-----------------

-  Появились методы :doc:`http/Recognize` и :doc:`http/GetRecognized`, позволяющие использовать Диадок для распознавания печатных форм счетов-фактур. Печатная форма подается на вход метода Recognize в формате `XPS <https://msdn.microsoft.com/en-us/library/windows/hardware/dn641615(v=vs.85).aspx>`__.

    В случае успешного распознавания на выходе метода GetRecognized получается XML-файл счета-фактуры в формате, удовлетворяющем требованиям ФНС и пригодном для отправки в соответствии с порядком, утвержденным Минфином РФ.

v0.6 - 26.08.2011
-----------------

-  В патчи с уведомлениями о невозможности доставки (DFN), возникающими по причине невалидности подписей под передаваемыми документами, теперь добавляются так называемые протоколы проверки подписей в виде отдельных сущностей для каждой подписи. Эти сущности-протоколы имеют тип :doc:`Attachment/SignatureVerificationReport <proto/Entity message>` и привязываться к «своим» подписям при помощи поля Entity.ParentEntityId. Протоколы проверки формируются для всех подписей (как валидных, так и невалидных), поэтому чтобы понять, какие именно подписи были признаны недействительными, нужно анализировать содержимое соответствующих протоколов. Содержимое сущности-протокола (массив байтов Entity.Content.Data) представляет собой сериализованную в протобуфер структуру :doc:`proto/SignatureVerificationResult`.

v0.5 - 15.08.2011
-----------------

-  Появилась возможность запрашивать формирование ЭП под пересылаемыми данными "по доверенности". В этом случае изготавливать ЭП на клиенте  не нужно (и значит, можно не устанавливать на рабочее место криптопровайдер), вместо этого формирование необходимой подписи будет произведено на сервере в момент доставки отправленного сообщения.

Изменения отразились в структурах данных :doc:`proto/MessageToPost` и :doc:`proto/MessagePatchToPost`.

v0.4 - 08.07.2011
-----------------

Появилась возможность формирования печатных форм различных документов (в частности, счетов фактур) при помощи метода :doc:`http/GeneratePrintForm`.

v0.3 - 17.06.2011
-----------------

-  Появилась возможность связывать документы в разных сообщениях. Для организации такой связи вводится структура данных :doc:`proto/DocumentId`, которую можно заполнить, например, в структуре :doc:`proto/XmlDocumentAttachment` при отправке корректировочного счета-фактуры.

    DocumentId включает в себя два идентификатора: поле DocumentId.MessageId - это идентификатор сообщения, содержащего исходный документ; поле DocumentId.EntityId - это идентификатор сущности, представляющей исходный документ в этом сообщении.

-  Появилась возможность отправить через API отказ от запрошенной подписи. Для этого в структуре :doc:`proto/MessagePatchToPost` появилось необязательное поле RequestedSignatureRejections.

-  Появилась возможность отслеживания отдельных документов при отправке их через черновики. Для этого метод PostDraft начал возвращать вместе с идентификатором черновика еще и идентификатор сущности, в которую превращается загруженный документ.

-  Уведомления о невозможности доставки теперь ссылаются на недоставленные куски сообщения.

    -  Для этого в структуре :doc:`Entity <proto/Entity message>` появилось необязательное поле NotDeliveredEventId. NotDeliveredEventId - это идентификатор сообщения или патча, который не удалось доставить (например, из-за некорректности одной или нескольких подписей в нем).

    -  Получить недоставленный кусок сообщения можно при помощи метода :doc:`http/GetEvent`, передав ему в качестве параметра eventId значение NotDeliveredEventId. Данное поле заполняется только у сущности типа Attachment с типом вложения DeliveryFailureNotification.

v0.2.2 - 15.04.2011
-------------------

Справочные методы GetBoxInfo, GetBoxesByAuthToken и GetBoxesByInnKpp научились отдавать данные в формате XML.

v0.2.1 - 07.04.2011
-------------------

Появилась возможность создавать черновики при помощи метода PostDraft.

v0.2 - 30.03.2011
-----------------

Появилась возможность вести документооборот по счетам-фактурам в соответствии с порядком Минфина.

v0.1.1 - 18.02.2011
-------------------

-  Появились методы для получения справочной информации GetBoxInfo и GetBoxesByInnKpp.

-  Появился метод для получения контента вложений по отдельности — :doc:`http/GetEntityContent`.

-  Метод :doc:`http/GetMessage` перестал отдавать весь тяжелый контент скопом (свыше 1Мб). Нужно учиться использовать метод :doc:`http/GetEntityContent`.

v0.1 - 09.12.2010
-----------------

Первоначальный релиз интеграторского интерфейса.
