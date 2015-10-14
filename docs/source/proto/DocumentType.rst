DocumentType
============

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
    }

Представляет тип документа.

-  *Nonformalized* - неформализованный документ.

-  *Invoice* - счет-фактура.

-  *InvoiceRevision* - исправление счета-фактуры.

-  *InvoiceCorrection* - корректировочный счет-фактура.

-  *InvoiceCorrectionRevision* - исправление корректировочного счета-фактуры.

-  *TrustConnectionRequest* - запрос на инициацию канала обмена документами через Диадок.

-  *Torg12* - товарная накладная ТОРГ-12.

-  *AcceptanceCertificate* - акт о выполении работ / оказании услуг.

-  *ProformaInvoice* - счет на оплату.

-  *XmlTorg12* - товарная накладная ТОРГ-12 в XML-формате.

-  *XmlAcceptanceCertificate* - акт о выполении работ / оказании услуг в XML-формате.

-  *PriceList* - ценовой лист.

-  *PriceListAgreement* - протокол согласования цены.

-  *CertificateRegistry* - реестр сертификатов.

-  *ReconciliationAct* - акт сверки.

-  *Contract* - договор.

-  *Torg13* - накладная ТОРГ-13.

-  *ServiceDetails* - детализация.

-  *SupplementaryAgreement* - дополнительное соглашение к договору.

-  *UnknownDocumentType* - неизвестный тип документа; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать тип документа, переданный сервером.
