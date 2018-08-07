UniversalDocumentMetadata
=========================

.. code-block:: protobuf

    message UniversalTransferDocumentMetadata {
        optional UniversalTransferDocumentStatus DocumentStatus = 1 [default = UnknownDocumentStatus];
        required string Total = 2; // TotalSum;
        optional string Vat = 3; //TotalVat;
        optional string Grounds = 4; // DocumentGrounds
        required string DocumentFunction = 5;
        required int32 Currency = 6;
        optional sfixed64 ConfirmationDateTimeTicks = 8;
        optional int32 InvoiceAmendmentFlags = 9;
    }

    message UniversalTransferDocumentRevisionMetadata {
        required UniversalTransferDocument.UniversalTransferDocumentStatus DocumentStatus = 1;
        required string Total = 2; // TotalSum;
        optional string Vat = 3; //TotalVat;
        optional string Grounds = 4; // DocumentGrounds
        required string DocumentFunction = 5;
        required int32 Currency = 6;
        optional sfixed64 ConfirmationDateTimeTicks = 7;
        required int32 InvoiceAmendmentFlags = 8;
        required string OriginalInvoiceNumber = 9;
        required string OriginalInvoiceDate = 10;
    }

    message UniversalCorrectionDocumentMetadata {
        required UniversalTransferDocument.UniversalTransferDocumentStatus DocumentStatus = 1;
        required string TotalInc = 2;
        required string TotalDec = 3;
        required string VatInc = 4;
        required string VatDec = 5;
        optional string Grounds = 6; // DocumentGrounds
        required string DocumentFunction = 7;
        required int32 Currency = 8;
        required sfixed64 ConfirmationDateTimeTicks = 9;
        required int32 InvoiceAmendmentFlags = 10;
        required string OriginalInvoiceNumber = 11;
        required string OriginalInvoiceDate = 12;
        optional string OriginalInvoiceRevisionNumber = 13;
        optional string OriginalInvoiceRevisionDate = 14;
    }

    message UniversalCorrectionDocumentRevisionMetadata {
        required UniversalTransferDocument.UniversalTransferDocumentStatus DocumentStatus = 1;
        required string TotalInc = 2;
        required string TotalDec = 3;
        required string VatInc = 4;
        required string VatDec = 5;
        optional string Grounds = 6; // DocumentGrounds
        required string DocumentFunction = 7;
        required int32 Currency = 8;
        required sfixed64 ConfirmationDateTimeTicks = 9;
        required int32 InvoiceAmendmentFlags = 10;
        required string OriginalInvoiceNumber = 11;
        required string OriginalInvoiceDate = 12;
        optional string OriginalInvoiceRevisionNumber = 13;
        optional string OriginalInvoiceRevisionDate = 14;
        required string OriginalInvoiceCorrectionNumber = 15;
        required string OriginalInvoiceCorrectionDate = 16;
    }

    enum UniversalTransferDocumentStatus {
        UnknownDocumentStatus = 0;  // This type will be reported to legacy client when it receives unknown status from server
        OutboundWaitingForSenderSignature = 1;
        OutboundWaitingForInvoiceReceiptAndRecipientSignature = 2;
        OutboundWaitingForInvoiceReceipt = 3; 
        OutboundWaitingForRecipientSignature = 4;
        OutboundWithRecipientSignature = 5;
        OutboundRecipientSignatureRequestRejected = 6;
        OutboundInvalidSenderSignature = 7;
        OutboundNotFinished = 8;
        OutboundFinished = 9;

        InboundWaitingForRecipientSignature = 16;
        InboundWithRecipientSignature = 17;
        InboundRecipientSignatureRequestRejected = 18;
        InboundInvalidRecipientSignature = 19;
        InboundNotFinished = 20;
        InboundFinished = 21;
    }

Структура данных *UniversalTransferDocumentMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`../Document`) специфичные для УПД:

-  *DocumentStatus* определяет состояние, в котором находится документооборот по данному УПД; принимает одно из значений перечисления *UniversalTransferDocumentStatus*.

-  *Total* - сумма УПД (берется из самого файла УПД).

-  *Vat* - сумма НДС УПД (берется из самого файла УПД).

-  *Grounds* - основания для первичного документа; представляются в виде неформализованной строки текста, например, "Договор №1234, Заказ №321".

-  *DocumentFunction* - 

-  *Currency* - код валюты УПД (берется из самого файла УПД).

-  *ConfirmationDateTimeTicks* - метка времени подтверждения оператора ДО об отправке исходящего УПД или о доставке входящего УПД. Представляет собой целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001. Данная метка представляет момент времени в московском часовом поясе (GMT+4).

-  :doc:`../InvoiceAmendmentFlags` отражает статус данного УПД:

    -  было ли затребовано уточнение, передавалось ли исправление УПД, передавался ли УКД;
    
    -  представляет собой битовую маску, составленную из одного или нескольких значений перечисления :doc:`../InvoiceAmendmentFlags`.

Структура данных *UniversalTransferDocumentRevisionMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`../Document`) специфичные для исправлений УПД:

-  *DocumentStatus* определяет состояние, в котором находится документооборот по данному исправлению УПД; принимает одно из значений перечисления *UniversalTransferDocumentStatus*.

-  *OriginalInvoiceNumber* - номер исходного УПД (берется из самого файла исправления УПД).

-  *OriginalInvoiceDate* - дата исходного УПД в формате ДД.ММ.ГГГГ (берется из самого файла исправления УПД).

-  *Total* - сумма исправления УПД (берется из самого файла исправления УПД).

-  *Vat* - сумма НДС исправления УПД (берется из самого файла исправления УПД).

-  *Grounds* - основания для первичного документа; представляются в виде неформализованной строки текста, например, "Договор №1234, Заказ №321".

-  *DocumentFunction* - 

-  *Currency* - код валюты исправления УПД (берется из самого файла исправления УПД).

-  *ConfirmationDateTimeTicks* - метка времени подтверждения оператора ДО об отправке исходящего исправления УПД или о доставке входящего исправления УПД.
   Представляет собой целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001. Данная метка представляет момент времени в московском часовом поясе (GMT+4).

-  :doc:`../InvoiceAmendmentFlags` отражает статус данного исправления УПД:

    -  было ли затребовано уточнение, передавалось ли исправление УПД, передавался ли УКД;
    
    -  представляет собой битовую маску, составленную из одного или нескольких значений перечисления :doc:`../InvoiceAmendmentFlags`.

Структура данных *UniversalCorrectionDocumentMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`../Document`) специфичные для УКД:

-  *DocumentStatus* определяет состояние, в котором находится документооборот по данному УКД; принимает одно из значений перечисления *UniversalTransferDocumentStatus*.

-  *OriginalInvoiceNumber* - номер исходного УПД (берется из самого файла УКД).

-  *OriginalInvoiceDate* - дата исходного УПД в формате ДД.ММ.ГГГГ (берется из самого файла УКД).

-  *OriginalInvoiceRevisionNumber* - номер исходного исправления УПД (берется из самого файла УКД, может отсутствовать).

-  *OriginalInvoiceRevisionDate* - дата исходного исправления УКД в формате ДД.ММ.ГГГГ (берется из самого файла УКД, может отсутствовать).

-  *TotalInc* - сумма к доплате УКД (берется из самого файла УКД).

-  *TotalDec* - сумма к уменьшению УКД (берется из самого файла УКД).

-  *VatInc* - сумма НДС к доплате УКД (берется из самого файла УКД).

-  *VatDec* - сумма НДС к уменьшению УКД (берется из самого файла УКД).

-  *Grounds* - основания для первичного документа; представляются в виде неформализованной строки текста, например, "Договор №1234, Заказ №321".

-  *DocumentFunction* - 

-  *Currency* - код валюты УКД (берется из самого файла УКД).

-  *ConfirmationDateTimeTicks* - метка времени подтверждения оператора ДО об отправке исходящего КСФ или о доставке входящего КСФ.
    
    -  Представляет собой целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001.
    
    -  Данная метка представляет момент времени в московском часовом поясе (GMT+4).

-  :doc:`../InvoiceAmendmentFlags` отражает статус данного УКД:

    -  было ли затребовано уточнение, передавалось ли исправление УКД;
    
    -  представляет собой битовую маску, составленную из одного или нескольких значений перечисления :doc:`../InvoiceAmendmentFlags`.

Структура данных *UniversalCorrectionDocumentRevisionMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`../Document`) специфичные для исправлений УКД:

-  *DocumentStatus* определяет состояние, в котором находится документооборот по данному исправлению УКД; принимает одно из значений перечисления *UniversalTransferDocumentStatus*.

-  *OriginalInvoiceNumber* - номер исходного УПД (берется из самого файла исправления УКД).

-  *OriginalInvoiceDate* - дата исходного УПД в формате ДД.ММ.ГГГГ (берется из самого файла исправления УКД).

-  *OriginalInvoiceRevisionNumber* - номер исходного исправления УПД (берется из самого файла исправления УКД, может отсутствовать).

-  *OriginalInvoiceRevisionDate* - дата исходного исправления УПД в формате ДД.ММ.ГГГГ (берется из самого файла исправления УКД,
   может отсутствовать).

-  *OriginalInvoiceCorrectionNumber* - номер исходного УКД (берется из самого файла исправления УКД).

-  *OriginalInvoiceCorrectionDate* - дата исходного УКД в формате ДД.ММ.ГГГГ (берется из самого файла исправления УКД).

-  *TotalInc* - сумма к доплате исправления УКД (берется из самого файла исправления УКД).

-  *TotalDec* - сумма к уменьшению исправления УКД (берется из самого файла исправления УКД).

-  *VatInc* - сумма НДС к доплате исправления УКД (берется из самого файла исправления УКД).

-  *VatDec* - сумма НДС к уменьшению исправления УКД (берется из самого файла исправления УКД).

-  *Grounds* - основания для первичного документа; представляются в виде неформализованной строки текста, например, "Договор №1234, Заказ №321".

-  *DocumentFunction* - 

-  *Currency* - код валюты исправления УКД (берется из самого файла исправления УКД).

-  *ConfirmationDateTimeTicks* - метка времени подтверждения оператора ДО об отправке исходящего исправления УКД или о доставке входящего исправления УКД.
    -  Представляет собой целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001.
    
    -  Данная метка представляет момент времени в московском часовом поясе (GMT+4).

-  :doc:`../InvoiceAmendmentFlags` отражает статус данного исправления УКД:

    -  было ли затребовано уточнение, передавалось ли исправления УКД;
    
    -  представляет собой битовую маску, составленную из одного или нескольких значений перечисления :doc:`../InvoiceAmendmentFlags`.

Перечисление *UniversalTransferDocumentStatus* задает возможные варианты состояний, в которых может находиться УПД/ИУПД/УКД/ИУКД:

-  *UnknownDocumentStatus* - неизвестный статус; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать статус документа, переданный сервером,

-  *OutboundWaitingForSenderSignature* - документ исходящий, документ не отправлен, поскольку не подписан отправителем,

-  *OutboundWaitingForInvoiceReceiptAndRecipientSignature* - документ исходящий, от покупателя ожидается извещение о получении УПД/ИУПД/УКД/ИУКД, ответная подпись, либо отказ от ее формирования,

-  *OutboundWaitingForInvoiceReceipt* - документ исходящий, ожидается извещение о получении УПД/ИУПД/УКД/ИУКД от покупателя,

-  *OutboundWaitingForRecipientSignature* - документ исходящий, ответная подпись, либо отказ от ее формирования еще не получены,

-  *OutboundWithRecipientSignature* - документ исходящий, ответная подпись получена,

-  *OutboundRecipientSignatureRequestRejected* - документ исходящий, получен отказ от формирования ответной подписи,

-  *OutboundInvalidSenderSignature* - документ исходящий, документ не отправлен, поскольку подпись отправителя не является корректной,

-  *OutboundFinished* - документ исходящий, документооборот завершен,

-  *OutboundNotFinished* - документ исходящий, извещение о получении УПД/ИУПД/УКД/ИУКД от покупателя уже есть, но документооборот еще не завершен,


-  *InboundWaitingForRecipientSignature* (документ входящий, ответная подпись, либо отказ от ее формирования еще не отправлены),

-  *InboundWithRecipientSignature* (документ входящий, ответная подпись поставлена),

-  *InboundRecipientSignatureRequestRejected* (документ входящий, отправлен отказ от формирования ответной подписи),

-  *InboundInvalidRecipientSignature* (документ входящий, документооборот не завершен, поскольку подпись получателя не является корректной),

-  *InboundNotFinished* (документ входящий, документооборот не завершен),

-  *InboundFinished* (документ входящий, документооборот завершен).


Статус рассчитывается без учета уведомлений об уточнении и извещений об их получении.
