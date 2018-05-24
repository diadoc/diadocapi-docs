Docflow
=======

.. code-block:: protobuf

    message Docflow
    {
        optional bool IsFinished = 1;
        optional SignedAttachment DocumentAttachment = 2;
        optional string DepartmentId = 3;
        optional bool DocumentIsDeleted = 4;
        optional DocflowStatus DocflowStatus = 5;
        optional Timestamp SendTimestamp = 6;
        optional Timestamp DeliveryTimestamp = 7;
        optional InboundInvoiceDocflow InboundInvoiceDocflow = 8;
        optional OutboundInvoiceDocflow OutboundInvoiceDocflow = 9;
        optional XmlBilateralDocflow XmlBilateralDocflow = 10;
        optional BilateralDocflow BilateralDocflow = 11;
        optional UnilateralDocflow UnilateralDocflow = 12;
        optional RevocationDocflow RevocationDocflow = 13;
        optional ResolutionDocflow ResolutionDocflow = 14;
        optional bool CanDocumentBeRevokedUnilaterallyBySender = 15;
        optional string PacketId = 16;
        repeated CustomDataItem CustomData = 17;
        optional InboundUniversalTransferDocumentDocflow InboundUniversalTransferDocumentDocflow = 18;
        optional OutboundUniversalTransferDocumentDocflow OutboundUniversalTransferDocumentDocflow = 19;
        optional RoamingNotification RoamingNotification = 20;
    }

Структура представляет состояние документооборота для одного документа.

-  *IsFinished* - признак того, что документооборот завершен, т.е. документ не требует дальнейших действий.

-  :doc:`DocumentAttachment <SignedAttachment>` - базовые данные о файле документа и подписи под ним.

-  *DepartmentId* - идентификатор подразделения, где в данный момент находится документ.

-  *DocumentIsDeleted* - признак того, что документ удален.

-  :doc:`DocflowStatus` - текущий статус документа (в соответствии с тем, на какой стадии находится его документооборот).

-  :doc:`SendTimestamp <Timestamp>` - метка времени отправки документа.

-  :doc:`DeliveryTimestamp <Timestamp>` - метка времени доставки документа.

-  Поля, заполняющиеся в зависимости от типа документа:

   -  :doc:`InboundInvoiceDocflow` - документооборот входящего счёта-фактуры (для документов типа *Invoice*, *InvoiceRevision*, *InvoiceCorrection*, *InvoiceCorrectionRevision*).

   -  :doc:`OutboundInvoiceDocflow` - документооборот исходящего счёта-фактуры (для документов типа *Invoice*, *InvoiceRevision*, *InvoiceCorrection*, *InvoiceCorrectionRevision*).

   -  :doc:`XmlBilateralDocflow` - документооборот двустороннего формализованного документа (для документов типа *XmlTorg12* или *XmlAcceptanceCertificate*).

   -  :doc:`BilateralDocflow` - документооборот двустороннего неформализованного документа (для документов типа *Nonformalized*, *Torg12*, *AcceptanceCertificate*, *TrustConnectionRequest*, *PriceList*, *PriceListAgreement*, *CertificateRegistry*, *ReconciliationAct*, *Contract*, *Torg13*).

   -  :doc:`UnilateralDocflow` - документооборот одностороннего неформализованного документа (для документов типа *ProformaInvoice*, *ServiceDetails*).

   -  :doc:`utd/docflow/InboundUniversalTransferDocumentDocflow` - документооборот входящего УПД (для документов типа *UniversalTransferDocument*, *UniversalTransferDocumentRevision*, *UniversalCorrectionDocument*, *UniversalCorrectionDocumentRevision*).

   -  :doc:`utd/docflow/OutboundUniversalTransferDocumentDocflow` - документооборот исходящего УПД (для документов типа *UniversalTransferDocument*, *UniversalTransferDocumentRevision*, *UniversalCorrectionDocument*, *UniversalCorrectionDocumentRevision*).

-  :doc:`RevocationDocflow` - данные об отзыве и аннулировании документа.

-  ``ResolutionDocflow`` - данные о согласовании документа.

-  *CanDocumentBeRevokedUnilaterallyBySender* - признак того, что документ может быть отозван отправителем в одностороннем порядке.

-  *PacketId* - идентификатор пакета, в котором в данный момент находится документ.

-  :doc:`CustomData <CustomDataItem>` - пользовательские данные, привязанные к документу.

-  :doc:`RoamingNotification <Docflow_RoamingNotification>` - данные о доставке документа в роуминг.