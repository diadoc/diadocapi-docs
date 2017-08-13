BilateralDocumentMetadata
=========================

.. code-block:: protobuf

    message TrustConnectionRequestMetadata {
        optional BilateralDocumentStatus TrustConnectionRequestStatus = 1 [default = UnknownBilateralDocumentStatus];
    }

    message BasicDocumentMetadata {
        optional BilateralDocumentStatus DocumentStatus = 1 [default = UnknownBilateralDocumentStatus];
        required string Total = 2;
        optional string Vat = 3;
        optional string Grounds = 4;
        optional ReceiptStatus ReceiptStatus = 5 [default = UnknownReceiptStatus];
    }

    message PriceListMetadata {
        required BilateralDocumentStatus DocumentStatus = 1;
        optional string PriceListEffectiveDate = 2;
        optional string ContractDocumentDate = 3;
        optional string ContractDocumentNumber = 4;
    }

    message ContractMetadata {
        optional BilateralDocumentStatus DocumentStatus = 1 [default = UnknownBilateralDocumentStatus];
        optional string ContractPrice = 2;
        optional string ContractType = 3;
        optional ReceiptStatus ReceiptStatus = 4 [default = UnknownReceiptStatus];
    }

    message BilateralDocumentMetadata {
        optional BilateralDocumentStatus DocumentStatus = 1 [default = UnknownBilateralDocumentStatus];
        optional ReceiptStatus ReceiptStatus = 2 [default = UnknownReceiptStatus];
    }

    enum BilateralDocumentStatus {
        UnknownBilateralDocumentStatus = 0;
        OutboundWaitingForRecipientSignature = 1;
        OutboundWithRecipientSignature = 2;
        OutboundRecipientSignatureRequestRejected = 3;
        OutboundWaitingForSenderSignature = 10;
        OutboundInvalidSenderSignature = 11;
        InboundWaitingForRecipientSignature = 4;
        InboundWithRecipientSignature = 5;
        InboundRecipientSignatureRequestRejected = 6;
        InboundInvalidRecipientSignature = 12;
        InternalWaitingForRecipientSignature = 7;
        InternalWithRecipientSignature = 8;
        InternalRecipientSignatureRequestRejected = 9;
        InternalWaitingForSenderSignature = 13;
        InternalInvalidSenderSignature = 14;
        InternalInvalidRecipientSignature = 15;
    }

    enum ReceiptStatus {
        UnknownReceiptStatus = 0; // Reserved state to report to legacy client for new statuses
        ReceiptStatusNone = 1;
        ReceiptStatusFinished = 2;
        ReceiptStatusHaveToCreateReceipt = 3;
        ReceiptStatusWaitingForReceipt = 4;
    }

    message AcceptanceCertificateMetadata {
        optional AcceptanceCertificateDocumentStatus DocumentStatus = 1 [default = UnknownAcceptanceCertificateDocumentStatus];
        required string Total = 2;
        optional string Vat = 3;
        optional string Grounds = 4;
        optional ReceiptStatus ReceiptStatus = 5 [default = UnknownReceiptStatus];
    }

    enum AcceptanceCertificateDocumentStatus {
        UnknownAcceptanceCertificateDocumentStatus = 0; // Reserved status to report to legacy clients for newly introduced statuses
        OutboundWaitingForRecipientSignature = 1;
        OutboundWithRecipientSignature = 2;
        OutboundRecipientSignatureRequestRejected = 3;
        OutboundWaitingForSenderSignature = 10;
        OutboundInvalidSenderSignature = 11;
        OutboundNoRecipientSignatureRequest = 16;
        InboundWaitingForRecipientSignature = 4;
        InboundWithRecipientSignature = 5;
        InboundRecipientSignatureRequestRejected = 6;
        InboundInvalidRecipientSignature = 12;
        InboundNoRecipientSignatureRequest = 17;
        InternalWaitingForRecipientSignature = 7;
        InternalWithRecipientSignature = 8;
        InternalRecipientSignatureRequestRejected = 9;
        InternalWaitingForSenderSignature = 13;
        InternalInvalidSenderSignature = 14;
        InternalInvalidRecipientSignature = 15;
        InternalNoRecipientSignatureRequest = 18;
    }

    message SupplementaryAgreementMetadata {
        optional BilateralDocumentStatus DocumentStatus = 1 [default = UnknownBilateralDocumentStatus];
        optional string Total = 2;
        optional string ContractType = 3;
        required string ContractNumber = 4;
        required string ContractDate = 5;
        optional ReceiptStatus ReceiptStatus = 6 [default = UnknownReceiptStatus];
    }

    Enum UniversalTransferDocumentStatus {
        UnknownDocumentStatus = 0;
        OutboundWaitingForSenderSignature = 1;
        OutboundWaitingForInvoiceReceiptAndRecipientSignature = 2;
        OutboundWaitingForInvoiceReceipt = 3; 
        OutboundWaitingForRecipientSignature = 4;
        OutboundInvalidSenderSignature = 5;
        InboundWaitingForInvoiceReceiptAndRecipientSignature = 6;
        InboundWaitingForRecipientSignature = 7; 
        InboundWaitingForInvoiceReceipt = 8;
        InboundWithRecipientSignature = 9; 
        InboundInvalidRecipientSignature = 10;
    }
        

Структура *BasicDocumentMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`Document`) специфичные для двусторонних первичных бухгалтерских документов (например, для товарных накладных ТОРГ-12):

-  *DocumentStatus* определяет состояние, в котором находится данный первичный документ; принимает одно из значений перечисления *BilateralDocumentStatus*

-  *Total* - сумма первичного документа.

-  *Vat* - сумма НДС первичного документа; если поле не заполнено, это значит что первичный документ в Диадоке был создан с отметкой "без НДС".

-  *Grounds* - основания для первичного документа; представляются в виде неформализованной строки текста, например, "Договор №1234, Заказ №321".

Структура *TrustConnectionRequestMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`Document`) специфичные для документов типа *TrustConnectionRequest*:

-  *TrustConnectionRequestStatus* определяет состояние, в котором находится данный документ; принимает одно из значений перечисления BilateralDocumentStatus.

Структура *PriceListMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`Document`) специфичные для ценовых листов:

-  *DocumentStatus* определяет состояние, в котором находится данный ценовой лист; принимает одно из значений перечисления BilateralDocumentStatus.

-  *PriceListEffectiveDate* - дата вступления в силу ценового листа в формате ДД.ММ.ГГГГ.

-  *ContractDocumentDate* - дата составления договора, к которому относится ценовой лист, в формате ДД.ММ.ГГГГ.

-  *ContractDocumentNumber* - номер договора, к которому относится ценовой лист.

Структура *BilateralDocumentMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`Document`):

-  *DocumentStatus* определяет состояние, в котором находится данный документ; принимает одно из значений перечисления BilateralDocumentStatus.

Структура *ContractMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`Document`), специфичные для договоров:

-  *DocumentStatus* определяет состояние, в котором находится данный документ; принимает одно из значений перечисления BilateralDocumentStatus.

-  *ContractType* - тип договора.

-  *ContractPrice* - цена, указанная в договоре.

Структура *SupplementaryAgreementMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`Document`), специфичные для дополнительного соглашения к договору:

-  *DocumentStatus* определяет состояние, в котором находится данный документ; принимает одно из значений перечисления *BilateralDocumentStatus*.

-  *Total* - цена дополнительного соглашения к договору.

-  *ContractType* - тип договора.

-  *ContractNumber* - номер договора.

-  *ContractDate* - дата договора.

Перечисление *BilateralDocumentStatus* задает возможные варианты состояний, в которых может находиться двусторонний документ (например, товарная накладная):

-  *UnknownBilateralDocumentStatus* (неизвестное состояние документа, может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать состояние документа, переданное сервером),

-  *OutboundWaitingForRecipientSignature* (документ исходящий, ответная подпись, либо отказ от ее формирования еще не получены),

-  *OutboundWithRecipientSignature* (документ исходящий, ответная подпись получена),

-  *OutboundRecipientSignatureRequestRejected* (документ исходящий, получен отказ от формирования ответной подписи),

-  *OutboundWaitingForSenderSignature* (документ исходящий, документ не отправлен, поскольку не подписан отправителем),

-  *OutboundInvalidSenderSignature* (документ исходящий, документ не отправлен, поскольку подпись отправителя не является корректной),

-  *InboundWaitingForRecipientSignature* (документ входящий, ответная подпись, либо отказ от ее формирования еще не отправлены),

-  *InboundWithRecipientSignature* (документ входящий, ответная подпись поставлена),

-  *InboundRecipientSignatureRequestRejected* (документ входящий, отправлен отказ от формирования ответной подписи),

-  *InboundInvalidRecipientSignature* (документ входящий, документооборот не завершен, поскольку подпись получателя не является корректной),

-  *InternalWaitingForRecipientSignature* (документ внутренний, ответная подпись, либо отказ от ее формирования еще не отправлены),

-  *InternalWithRecipientSignature* (документ внутренний, ответная подпись поставлена),

-  *InternalRecipientSignatureRequestRejected* (документ внутренний, отправлен отказ от формирования ответной подписи),

-  *InternalWaitingForSenderSignature* (документ внутренний, документ не отправлен, поскольку не подписан отправителем),

-  *InternalInvalidSenderSignature* (документ внутренний, документ не отправлен, поскольку подпись отправителя не является корректной),

-  *InternalInvalidRecipientSignature* (документ внутренний, документооборот не завершен, поскольку подпись получателя не
   является корректной).

Структура *AcceptanceCertificateMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`Document`) специфичные для актов о выполнении работ / оказании услуг. Описание полей - аналогично структуре *BasicDocumentMetadata*, отличается только тип поля *DocumentStatus* (см. описание перечисления AcceptanceCertificateDocumentMetadata).

Перечисление *AcceptanceCertificateDocumentStatus* задает возможные варианты состояний, в которых может находиться акт о выполнении работ/оказании услуг. Содержит все значения из перечисления BilateralDocumentStatus и дополнительно еще несколько возможных значений:

-  *OutboundNoRecipientSignatureRequest* (документ исходящий, ответная подпись не запрошена),

-  *InboundNoRecipientSignatureRequest* (документ входящий, ответная подпись не запрошена),

-  *InternalNoRecipientSignatureRequest* (документ внутренний, ответная подпись не запрошена).

Перечисление *UniversalTransferDocumentStatus* задает возможные варианты состояний, в которых может находиться Универсальный передаточный документ (УПД). Содержит все значения из перечисления BilateralDocumentStatus и дополнительно еще несколько возможных значений:

-  *OutboundWaitingForInvoiceReceiptAndRecipientSignature* - документ исходящий, ожидается извещение о получении и подпись получателя,

-  *OutboundWaitingForInvoiceReceipt* = 3; - документ исходящий, ожидается извещение о получении,

-  *InboundWaitingForInvoiceReceiptAndRecipientSignature* - документ входящий, ожидается извещение о получении и подпись получателя,

-  *InboundWaitingForInvoiceReceipt* - документ входящий, ожидается извещение о получении.
