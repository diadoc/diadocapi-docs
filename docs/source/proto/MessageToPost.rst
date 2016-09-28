MessageToPost
=============

.. code-block:: protobuf

    message MessageToPost {
        required string FromBoxId = 1;
        optional string ToBoxId = 2;
        repeated XmlDocumentAttachment Invoices = 3;
        repeated NonformalizedAttachment NonformalizedDocuments = 4;
        repeated BasicDocumentAttachment Torg12Documents = 5;
        optional TrustConnectionRequestAttachment TrustConnectionRequest = 6;
        repeated BasicDocumentAttachment AcceptanceCertificates = 7;
        repeated StructuredDataAttachment StructuredDataAttachments = 8;
        repeated BasicDocumentAttachment ProformaInvoices = 9;
        repeated XmlDocumentAttachment XmlTorg12SellerTitles = 10;
        repeated XmlDocumentAttachment XmlAcceptanceCertificateSellerTitles = 11;
        optional string ToDepartmentId = 12;
        optional bool IsDraft = 13 [default = false];
        optional bool LockDraft = 14 [default = false];
        optional bool StrictDraftValidation = 15 [default = true];
        optional bool IsInternal = 16 [default = false];
        optional string FromDepartmentId = 17;
        optional bool DelaySend = 18 [default = false];
        repeated PriceListAttachment PriceLists = 19;
        repeated NonformalizedAttachment PriceListAgreements = 20;
        repeated NonformalizedAttachment CertificateRegistries = 21;
        repeated ReconciliationActAttachment ReconciliationActs = 22;
        repeated ContractAttachment Contracts = 23;
        repeated Torg13Attachment Torg13Documents = 24;
        repeated ServiceDetailsAttachment ServiceDetailsDocuments = 25;
        optional string ProxyBoxId = 26;
        optional string ProxyDepartmentId = 27;
        repeated EncryptedInvoiceAttachment EncryptedInvoices = 28;
        repeated EncryptedXmlDocumentAttachment EncryptedXmlTorg12SellerTitles = 29;
        repeated EncryptedXmlDocumentAttachment EncryptedXmlAcceptanceCertificateSellerTitles = 30;
        repeated SupplementaryAgreementAttachment SupplementaryAgreements = 31;
        optional bool LockPacket = 32 [default = false];
        repeated XmlDocumentAttachment UniversalTransferDocumentSellerTitles = 33;
    }
        

Структура данных *MessageToPost* представляет сообщение, подлежащее отправке через Диадок при помощи метода :doc:`../http/PostMessage`:

-  *FromBoxId* - идентификатор ящика отправителя сообщения.

-  *ToBoxId* - идентификатор ящика получателя сообщения. Должен отличаться от идентификатора ящика отправителя. Для внутреннего документа (IsInternal = true) этот идентификатор должен оставаться пустым (отсутствовать или содержать пустую строку).

-  *IsInternal* - флаг, показывающий, что сообщение является внутренним, то есть сообщением между подразделениями организации.

-  *ToDepartmentId* - идентификатор подразделения в организации получателя, в которое будут отправлены все документы из сообщения (может отсутствовать, в этом случае документы будут отправлены в головное подразделение)

-  *FromDepartmentId* - идентификатор подразделения отправителя сообщения.

-  :doc:`Invoices <XmlDocumentAttachment>` - список СФ/ИСФ/КСФ/ИКСФ (то есть документов, обмен которыми производится в соответствии с порядком Минфина) в отправляемом сообщении.

-  :doc:`NonformalizedDocuments <NonformalizedAttachment>` - список неформализованных документов в отправляемом сообщении.

-  :doc:`TrustConnectionRequest <TrustConnectionRequestAttachment>` - запрос на инициацию канала обмена документами через Диадок в отправляемом сообщении. Данная возможность устарела, для отправки приглашения с вложенным документов воспользуйтесь методом :doc:`../http/AcquireCounteragent`

-  :doc:`ProformaInvoices <BasicDocumentAttachment>` - список счетов на оплату в отправляемом сообщении.

-  :doc:`Torg12Documents <BasicDocumentAttachment>` - список товарных накладных ТОРГ-12 в отправляемом сообщении.

-  :doc:`AcceptanceCertificates <AcceptanceCertificateAttachment>` - список актов о выполнении работ (оказании услуг) в отправляемом сообщении.

-  :doc:`XmlTorg12SellerTitles <XmlDocumentAttachment>` - список титулов продавца для товарных накладных ТОРГ-12 в XML-формате в отправляемом сообщении.

-  :doc:`XmlAcceptanceCertificateSellerTitles <XmlDocumentAttachment>` - список титулов исполнителя для актов о выполнении работ (оказании услуг) в XML-формате в отправляемом сообщении.

-  :doc:`StructuredDataAttachments <StructuredDataAttachment>` - список файлов со структурированными данными в отправляемом сообщении,описывающими те или иные документы, представленные в виде печатных форм.

-  :doc:`PriceLists <PriceListAttachment>` - список ценовых листов в отправляемом сообщении.

-  :doc:`PriceListAgreements <NonformalizedAttachment>` - список протоколов согласования цены в отправляемом сообщении.

-  :doc:`CertificateRegistries <NonformalizedAttachment>` - список реестров сертификатов в отправляемом сообщении.

-  :doc:`ReconciliationActs <ReconciliationActAttachment>` - список актов сверки в отправляемом сообщении.

-  :doc:`Contracts <ContractAttachment>` - список договоров в отправляемом сообщении.

-  :doc:`Torg13Documents <Torg13Attachment>` - список накладных ТОРГ-13 в отправляемом сообщении.

-  :doc:`ServiceDetailsDocuments <ServiceDetailsAttachment>` - список детализаций в отправляемом сообщении.

-  :doc:`EncryptedInvoices <EncryptedInvoiceAttachment>` - список зашифрованных счетов-фактур в отправляемом сообщении.

-  :doc:`EncryptedXmlTorg12SellerTitles <EncryptedXmlDocumentAttachment>` - список зашифрованных формализованных накладных ТОРГ-12 в отправляемом сообщении.

-  :doc:`EncryptedXmlAcceptanceCertificateSellerTitles <EncryptedXmlDocumentAttachment>` - список зашифрованных формализованных актов о выполнении работ (оказании услуг) в отправляемом сообщении.

-  :doc:`SupplementaryAgreements <SupplementaryAgreementAttachment>` - список дополнительных соглашанеий к договорам в отправляемом сообщении.

-  :doc:`UniversalTransferDocumentSellerTitles <XmlDocumentAttachment>` - список титулов продавца универсального передаточного документа (УПД) в XML формате.

-  *ProxyBoxId* - идентификатор ящика, промежуточного получателя. Если указан ящик промежуточного получателя, то документа доставится конечному получателя только после того, как промежуточный получатель поставит подпись под документом. Если промежуточный получатель отклонит документ, то в ящик конечного получателя он не будет доставлен.

-  *ProxyDepartmentId* - идентификатор подразделения, в ящике промежуточного получателя.
   
-  *IsDraft* - флаг, показывающий, что данное сообщение является черновиком (возможно, содержит неподписанные документы), и не подлежит отправке. Для добавления подписей к черновику и его отправки следует использовать метод :doc:`../http/SendDraft`.

-  *LockDraft* - флаг, показывающий, что данный черновик является защищенным от изменений.

-  *StrictDraftValidation* - флаг, включающий проверку правильности черновика (по умолчанию проверка включена).

-  *DelaySend* - флаг, означает, что документ из сообщения будет сохранен без отправки.

-  *LockPacket* - флаг, означает, что документы сообщения будут отправлены закрытым пакетом. В таком пакете любая операция применяется ко всем документам сразу.

Сообщения с флагом *DelaySend*, должны удовлетворять следующим 

-  Подпись под документом и запрос на подпись по доверенности должны отсутствовать.

Это не черновик, поэтому ни содержимое документа, ни реквизиты получателя нельзя будет поменять в дальнейшем.

Сохраненные таким образом документы можно будет найти, используя метод :doc:`../http/GetDocuments`. Также можно их согласовывать, используя :doc:`../http/PostMessagePatch` или через веб-интерфейс.

После того как обработка на стороне отправителя больше не требуется, то документ можно подписать и отправить. Пока это можно сделать только через веб-интерфейс.

По умолчанию, все документы переданные одним сообщением будут связаны в пакет.
