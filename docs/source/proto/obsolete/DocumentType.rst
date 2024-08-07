DocumentType
============

.. warning::
	Перечисление устарело. Чтобы получить тип и версию документа, используйте метод :doc:`../../http/GetDocumentTypes`.

Перечисление ``DocumentType`` представляет собой тип документа.

.. code-block:: protobuf

    enum DocumentType
    {
        UnknownDocumentType = -1;
        Nonformalized = 0;
        Invoice = 1;
        TrustConnectionRequest = 11;
        Torg12 = 12;
        InvoiceRevision = 13;
        InvoiceCorrection = 14;
        InvoiceCorrectionRevision = 15;
        AcceptanceCertificate = 16;
        ProformaInvoice = 18;
        XmlTorg12 = 19;
        XmlAcceptanceCertificate = 20;
        PriceList = 26;
        PriceListAgreement = 30;
        CertificateRegistry = 34;
        ReconciliationAct = 35;
        Contract = 36;
        Torg13 = 37;
        ServiceDetails = 38;
        SupplementaryAgreement = 40;
        UniversalTransferDocument = 41;
        UniversalTransferDocumentRevision = 45;
        UniversalCorrectionDocument = 49;
        UniversalCorrectionDocumentRevision = 50;
    }

- ``UnknownDocumentType`` — неизвестный тип документа; возвращается только в устаревшей версии Docflow API.
- ``Nonformalized`` — неформализованный документ.
- ``Invoice`` — счет-фактура.
- ``InvoiceRevision`` — исправление счета-фактуры.
- ``InvoiceCorrection`` — корректировочный счет-фактура.
- ``InvoiceCorrectionRevision`` — исправление корректировочного счета-фактуры.
- ``TrustConnectionRequest`` — запрос на инициацию канала обмена документами через Диадок.
- ``Torg12`` — товарная накладная ТОРГ-12.
- ``AcceptanceCertificate`` — акт о выполнении работ / оказании услуг.
- ``ProformaInvoice`` — счет на оплату.
- ``XmlTorg12`` — товарная накладная ТОРГ-12 в XML-формате.
- ``XmlAcceptanceCertificate`` — акт о выполнении работ / оказании услуг в XML-формате.
- ``PriceList`` — ценовой лист.
- ``PriceListAgreement`` — протокол согласования цены.
- ``CertificateRegistry`` — реестр сертификатов.
- ``ReconciliationAct`` — акт сверки.
- ``Contract`` — договор.
- ``Torg13`` — накладная ТОРГ-13.
- ``ServiceDetails`` — детализация.
- ``SupplementaryAgreement`` — дополнительное соглашение к договору.
- ``UniversalTransferDocument`` — универсальный передаточный документ (УПД).
- ``UniversalTransferDocumentRevision`` — исправление универсального передаточного документа.
- ``UniversalCorrectionDocument`` — универсальный корректировочный документ (УКД).
- ``UniversalCorrectionDocumentRevision`` — исправление универсального корректировочного документа.


----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`../Document`
	- в устаревшей структуре :doc:`DocumentInfo`