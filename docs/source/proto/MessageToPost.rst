MessageToPost
=============

Структура ``MessageToPost`` представляет собой сообщение для отправки методом :doc:`../http/PostMessage`. По умолчанию все документы в сообщении будут связаны в пакет.

.. code-block:: protobuf

    message MessageToPost {
        required string FromBoxId = 1;
        optional string ToBoxId = 2;
        repeated XmlDocumentAttachment Invoices = 3;                                // Устаревшая структура
        repeated NonformalizedAttachment NonformalizedDocuments = 4;                // Устаревшая структура
        repeated BasicDocumentAttachment Torg12Documents = 5;                       // Устаревшая структура
        optional TrustConnectionRequestAttachment TrustConnectionRequest = 6;       // Устаревшая структура
        repeated AcceptanceCertificateAttachment AcceptanceCertificates = 7;        // Устаревшая структура
        repeated StructuredDataAttachment StructuredDataAttachments = 8;
        repeated BasicDocumentAttachment ProformaInvoices = 9;                      // Устаревшая структура
        repeated XmlDocumentAttachment XmlTorg12SellerTitles = 10;                  // Устаревшая структура
        repeated XmlDocumentAttachment XmlAcceptanceCertificateSellerTitles = 11;   // Устаревшая структура
        optional string ToDepartmentId = 12;
        optional bool IsDraft = 13 [default = false];
        optional bool LockDraft = 14 [default = false];
        optional bool StrictDraftValidation = 15 [default = true];
        optional bool IsInternal = 16 [default = false];
        optional string FromDepartmentId = 17;
        optional bool DelaySend = 18 [default = false];
        repeated PriceListAttachment PriceLists = 19;                               // Устаревшая структура
        repeated NonformalizedAttachment PriceListAgreements = 20;                  // Устаревшая структура
        repeated NonformalizedAttachment CertificateRegistries = 21;                // Устаревшая структура
        repeated ReconciliationActAttachment ReconciliationActs = 22;               // Устаревшая структура
        repeated ContractAttachment Contracts = 23;                                 // Устаревшая структура
        repeated Torg13Attachment Torg13Documents = 24;                             // Устаревшая структура
        repeated ServiceDetailsAttachment ServiceDetailsDocuments = 25;             // Устаревшая структура
        optional string ProxyBoxId = 26;
        optional string ProxyDepartmentId = 27;
        repeated EncryptedInvoiceAttachment EncryptedInvoices = 28;                 // Устаревшая структура
        repeated EncryptedXmlDocumentAttachment EncryptedXmlTorg12SellerTitles = 29; // Устаревшая структура
        repeated EncryptedXmlDocumentAttachment EncryptedXmlAcceptanceCertificateSellerTitles = 30; // Устаревшая структура
        repeated SupplementaryAgreementAttachment SupplementaryAgreements = 31;     // Устаревшая структура
        optional bool LockPacket = 32 [default = false];
        repeated XmlDocumentAttachment UniversalTransferDocumentSellerTitles = 33;  // Устаревшая структура
        repeated DocumentAttachment DocumentAttachments = 34;
        optional LockMode LockMode = 35 [default = None];
    }

- ``FromBoxId`` — идентификатор ящика отправителя сообщения.
- ``ToBoxId`` — идентификатор ящика получателя сообщения. Должен отличаться от идентификатора ящика отправителя. Для внутреннего сообщения (если при создании сообщения был указан флаг ``IsInternal = true``) этот идентификатор должен отсутствовать или содержать пустую строку.
- ``StructuredDataAttachments`` — список файлов со структурированными данными в отправляемом сообщении, описывающими документы, представленные в виде печатных форм. Представлены структурой :doc:`StructuredDataAttachment`.
- ``ToDepartmentId`` — идентификатор подразделения организации получателя, в которое будет отправлено сообщение. Необязательное поле. Если не заполнено, сообщение будет отправлено в головное подразделение.
- ``IsDraft`` — флаг, указывающий, что сообщение является :doc:`черновиком<../entities/draft>` и не подлежит отправке. Для добавления подписей к черновику и отправки используйте метод :doc:`../http/SendDraft`.
- ``LockDraft`` — флаг, указывающий, что черновик защищен от изменений.
- ``StrictDraftValidation`` — флаг, включающий проверку правильности черновика. По умолчанию проверка включена.
- ``IsInternal`` — флаг, указывающий, что сообщение является внутренним, то есть будет отправлено в другое подразделение организации.
- ``FromDepartmentId`` — идентификатор подразделения отправителя сообщения.
- ``DelaySend`` — флаг, указывающий, что документ из сообщения будет :ref:`сохранен без отправки<doc_delaysend>`.
- ``ProxyBoxId`` — идентификатор ящика промежуточного получателя. Если указан, сообщение будет доставлено конечному получателю после того, как промежуточный получатель поставит подпись под документом в сообщении. Если промежуточный получатель отклонит документ, сообщение не будет доставлено конечному получателю.
- ``ProxyDepartmentId`` — идентификатор подразделения промежуточного получателя.
- ``LockPacket`` — флаг, указывающий, что документы в сообщении будут отправлены закрытым пакетом. В закрытом пакете любая операция применяется ко всем документам. Эквивалентен ``LockMode = Full``.
- ``DocumentAttachments`` — список документов любых типов, представленных структурой :doc:`DocumentAttachment`.
- ``LockMode`` — режим блокировки сообщения, представленный перечислением :doc:`../proto/LockMode`.


Устаревшие поля
---------------

- ``Invoices`` — список СФ/ИСФ/КСФ/ИКСФ в отправляемом сообщении, представленных структурой :doc:`obsolete/XmlDocumentAttachment`.
- ``NonformalizedDocuments`` — список неформализованных документов в отправляемом сообщении, представленных структурой :doc:`obsolete/NonformalizedAttachment`.
- ``Torg12Documents`` — список товарных накладных ТОРГ-12 в отправляемом сообщении, представленных структурой :doc:`obsolete/BasicDocumentAttachment`.
- ``TrustConnectionRequest`` — приглашение контрагента к обмену документами через Диадок, представленное структурой :doc:`obsolete/TrustConnectionRequestAttachment`. Для отправки приглашения с вложенным документом используйте метод :doc:`../http/AcquireCounteragent`.
- ``AcceptanceCertificates`` — список актов о выполнении работ или оказании услуг, представленных структурой :doc:`obsolete/AcceptanceCertificateAttachment`.
- ``ProformaInvoices`` — список счетов на оплату в отправляемом сообщении, представленных структурой :doc:`obsolete/BasicDocumentAttachment`.
- ``XmlTorg12SellerTitles`` — список титулов продавца для товарных накладных ТОРГ-12 в XML-формате в отправляемом сообщении, представленных структурой :doc:`obsolete/XmlDocumentAttachment`.
- ``XmlAcceptanceCertificateSellerTitles`` — список титулов исполнителя для актов о выполнении работ или оказании услуг в XML-формате в отправляемом сообщении, представленных структурой :doc:`obsolete/XmlDocumentAttachment`.
- ``PriceLists`` — список ценовых листов в отправляемом сообщении, представленных структурой :doc:`obsolete/PriceListAttachment`.
- ``CertificateRegistries`` — список реестров сертификатов в отправляемом сообщении, представленных структурой :doc:`obsolete/NonformalizedAttachment`.
- ``ReconciliationActs`` — список актов сверки в отправляемом сообщении, представленных структурой :doc:`obsolete/ReconciliationActAttachment`.
- ``Contracts`` — список договоров в отправляемом сообщении, представленных структурой :doc:`obsolete/ContractAttachment`.
- ``Torg13Documents`` — список накладных ТОРГ-13 в отправляемом сообщении, представленных структурой :doc:`obsolete/Torg13Attachment`.
- ``ServiceDetailsDocuments`` — список детализаций в отправляемом сообщении, представленных структурой :doc:`obsolete/ServiceDetailsAttachment`.
- ``EncryptedInvoices`` — список зашифрованных счетов-фактур в отправляемом сообщении, представленных структурой :doc:`obsolete/EncryptedInvoiceAttachment` 
- ``EncryptedXmlTorg12SellerTitles`` — список зашифрованных формализованных накладных ТОРГ-12 в отправляемом сообщении, представленных структурой :doc:`obsolete/EncryptedXmlDocumentAttachment`.
- ``EncryptedXmlAcceptanceCertificateSellerTitles`` — список зашифрованных формализованных актов о выполнении работ или оказании услуг в отправляемом сообщении, представленных структурой :doc:`obsolete/EncryptedXmlDocumentAttachment`.
- ``SupplementaryAgreements`` — список дополнительных соглашений к договорам в отправляемом сообщении, представленных структурой :doc:`obsolete/SupplementaryAgreementAttachment`.
- ``UniversalTransferDocumentSellerTitles`` — список титулов продавца универсального передаточного документа (УПД) в XML формате, представленных структурой :doc:`obsolete/XmlDocumentAttachment`.


----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/PostMessage`