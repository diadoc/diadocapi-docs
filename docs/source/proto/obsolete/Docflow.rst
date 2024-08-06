Docflow
=======

.. warning::
	Структура устарела. Вместо нее используется структура :doc:`../DocflowV3`.

Структура ``Docflow`` представляет состояние документооборота для одного документа.

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

- ``IsFinished`` — признак того, что документооборот завершен и документ не требует дальнейших действий.
- ``DocumentAttachment`` — данные о файле документа и подписи под ним, представленные структурой :doc:`../SignedAttachment`.
- ``DepartmentId`` — идентификатор подразделения, в котором находится документ.
- ``DocumentIsDeleted`` — признак того, что документ удален.
- ``DocflowStatus`` — текущий статус документа, соответствующий стадии его документооборота, представленный структурой :doc:`DocflowStatus`.
- ``SendTimestamp`` — время отправки документа, представленное структурой :doc:`../Timestamp`.
- ``DeliveryTimestamp`` — время доставки документа, представленное структурой :doc:`../Timestamp`.
- ``CanDocumentBeRevokedUnilaterallyBySender`` — признак того, что документ может быть отозван отправителем в одностороннем порядке.
- ``PacketId`` — идентификатор пакета, в котором в данный момент находится документ.
- ``CustomData`` — список пользовательских данных (:doc:`тегов <../../entities/tag>`), привязанных к документу. Каждый тег представлен структурой :doc:`../CustomDataItem`.
- ``RoamingNotification`` — данные о доставке документа в роуминг, представленные структурой :doc:`../RoamingNotification`.

-  Поля, заполняющиеся в зависимости от типа документа:

   - ``InboundInvoiceDocflow`` — документооборот входящего счета-фактуры, представленный структурой :doc:`InboundInvoiceDocflow` — для документов с типом ``Invoice``, ``InvoiceRevision``, ``InvoiceCorrection``, ``InvoiceCorrectionRevision``.
   - ``OutboundInvoiceDocflow`` — документооборот исходящего счета-фактуры, представленный структурой :doc:`OutboundInvoiceDocflow` — для документов с типом ``Invoice``, ``InvoiceRevision``, ``InvoiceCorrection``, ``InvoiceCorrectionRevision``.
   - ``XmlBilateralDocflow`` — документооборот двустороннего формализованного документа, представленный структурой :doc:`XmlBilateralDocflow` — для документов с типом ``XmlTorg12`` или ``XmlAcceptanceCertificate``.
   - ``BilateralDocflow`` — документооборот двустороннего неформализованного документа, представленный структурой :doc:`BilateralDocflow` — для документов с типом ``Nonformalized``, ``Torg12``, ``AcceptanceCertificate``, ``TrustConnectionRequest``, ``PriceList``, ``PriceListAgreement``, ``CertificateRegistry``, ``ReconciliationAct``, ``Contract``, ``Torg13``.
   - ``UnilateralDocflow`` — документооборот одностороннего неформализованного документа, представленный структурой :doc:`UnilateralDocflow` — для документов с типом ``ProformaInvoice``, ``ServiceDetails``.
   - ``RevocationDocflow`` — информация об аннулировании документа, представлення структурой :doc:`RevocationDocflow`.
   - ``ResolutionDocflow`` — данные о согласовании документа. Поле устарело и не заполняется методами.
   - ``InboundUniversalTransferDocumentDocflow`` — документооборот входящего УПД, представленный структурой :doc:`InboundUniversalTransferDocumentDocflow` — для документов с типом ``UniversalTransferDocument``, ``UniversalTransferDocumentRevision``, ``UniversalCorrectionDocument``, ``UniversalCorrectionDocumentRevision``.
   - ``OutboundUniversalTransferDocumentDocflow`` — документооборот исходящего УПД, представленный структурой :doc:`OutboundUniversalTransferDocumentDocflow` — для документов с типом ``UniversalTransferDocument``, ``UniversalTransferDocumentRevision``, ``UniversalCorrectionDocument``, ``UniversalCorrectionDocumentRevision``.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`DocumentWithDocflow`