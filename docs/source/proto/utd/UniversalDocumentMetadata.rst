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

-  *Total* - сумма счета-фактуры (берется из самого файла СФ).

-  *Vat* - сумма НДС счета-фактуры (берется из самого файла СФ).

-  *Currency* - код валюты счета-фактуры (берется из самого файла СФ).

-  *ConfirmationDateTimeTicks* - метка времени подтверждения оператора ДО об отправке исходящего СФ или о доставке входящего СФ. Представляет собой целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001. Данная метка представляет момент времени в московском часовом поясе (GMT+4).

-  *InvoiceAmendmentFlags* отражает статус данного СФ: было ли затребовано уточнение, передавалось ли ИСФ, передавался ли КСФ;
   представляет собой битовую маску, составленную из одного или нескольких значений перечисления InvoiceAmendmentFlags.

Структура данных *InvoiceRevisionMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`../Document`) специфичные для исправлений счетов-фактур:

-  *InvoiceRevisionStatus* определяет состояние, в котором находится документооборот по данному ИСФ; принимает одно из значений перечисления *InvoiceStatus*.

-  *OriginalInvoiceNumber* - номер исходного счета-фактуры (берется из самого файла ИСФ).

-  *OriginalInvoiceDate* - дата исходного счета-фактуры в формате ДД.ММ.ГГГГ (берется из самого файла ИСФ).

-  *Total* - сумма исправления счета-фактуры (берется из самого файла ИСФ).

-  *Vat* - сумма НДС исправления счета-фактуры (берется из самого файла ИСФ).

-  *Currency* - код валюты исправления счета-фактуры (берется из самого файла ИСФ).

-  *ConfirmationDateTimeTicks* - метка времени подтверждения оператора ДО об отправке исходящего ИСФ или о доставке входящего ИСФ.
   Представляет собой целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001. Данная метка представляет момент времени в московском часовом поясе (GMT+4).

-  *InvoiceAmendmentFlags* отражает статус данного ИСФ: было ли затребовано уточнение, передавалось ли ИСФ, передавался ли КСФ;
   представляет собой битовую маску, составленную из одного или нескольких значений перечисления *InvoiceAmendmentFlags*.

Структура данных *InvoiceCorrectionMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`../Document`) специфичные для корректировочных счетов-фактур:

-  *InvoiceStatus* определяет состояние, в котором находится документооборот по данному КСФ; принимает одно из значений перечисления *InvoiceStatus*.

-  *OriginalInvoiceNumber* - номер исходного счета-фактуры (берется из самого файла КСФ).

-  *OriginalInvoiceDate* - дата исходного счета-фактуры в формате ДД.ММ.ГГГГ (берется из самого файла КСФ).

-  *OriginalInvoiceRevisionNumber* - номер исходного исправления счета-фактуры (берется из самого файла КСФ, может отсутствовать).

-  *OriginalInvoiceRevisionDate* - дата исходного исправления счета-фактуры в формате ДД.ММ.ГГГГ (берется из самого файла КСФ, может отсутствовать).

-  *TotalInc* - сумма к доплате корректировочного счета-фактуры (берется из самого файла КСФ).

-  *TotalDec* - сумма к уменьшению корректировочного счета-фактуры (берется из самого файла КСФ).

-  *VatInc* - сумма НДС к доплате корректировочного счета-фактуры (берется из самого файла КСФ).

-  *VatDec* - сумма НДС к уменьшению корректировочного счета-фактуры (берется из самого файла КСФ).

-  *Currency* - код валюты корректировочного счета-фактуры (берется из самого файла КСФ).

-  *ConfirmationDateTimeTicks* - метка времени подтверждения оператора ДО об отправке исходящего КСФ или о доставке входящего КСФ.
   Представляет собой целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001. Данная метка
   представляет момент времени в московском часовом поясе (GMT+4).

-  *InvoiceAmendmentFlags* отражает статус данного КСФ: было ли затребовано уточнение, передавалось ли ИКСФ; представляет собой битовую маску, составленную из одного или нескольких значений перечисления *InvoiceAmendmentFlags*.

Структура данных *InvoiceCorrectionRevisionMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`../Document`) специфичные для исправлений корректировочных счетов-фактур:

-  *InvoiceStatus* определяет состояние, в котором находится документооборот по данному ИКСФ; принимает одно из значений перечисления *InvoiceStatus*.

-  *OriginalInvoiceNumber* - номер исходного счета-фактуры (берется из самого файла ИКСФ).

-  *OriginalInvoiceDate* - дата исходного счета-фактуры в формате ДД.ММ.ГГГГ (берется из самого файла ИКСФ).

-  *OriginalInvoiceRevisionNumber* - номер исходного исправления счета-фактуры (берется из самого файла ИКСФ, может отсутствовать).

-  *OriginalInvoiceRevisionDate* - дата исходного исправления счета-фактуры в формате ДД.ММ.ГГГГ (берется из самого файла ИКСФ,
   может отсутствовать).

-  *OriginalInvoiceCorrectionNumber* - номер исходного корректировочного счета-фактуры (берется из самого файла ИКСФ).

-  *OriginalInvoiceCorrectionDate* - дата исходного корректировочного счета-фактуры в формате ДД.ММ.ГГГГ (берется из самого файла ИКСФ).

-  *TotalInc* - сумма к доплате исправления корректировочного счета-фактуры (берется из самого файла ИКСФ).

-  *TotalDec* - сумма к уменьшению исправления корректировочного счета-фактуры (берется из самого файла ИКСФ).

-  *VatInc* - сумма НДС к доплате исправления корректировочного счета-фактуры (берется из самого файла ИКСФ).

-  *VatDec* - сумма НДС к уменьшению исправления корректировочного счета-фактуры (берется из самого файла ИКСФ).

-  *Currency* - код валюты исправления корректировочного счета-фактуры (берется из самого файла ИКСФ).

-  *ConfirmationDateTimeTicks* - метка времени подтверждения оператора ДО об отправке исходящего ИКСФ или о доставке входящего ИКСФ.
   Представляет собой целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001. Данная метка представляет момент времени в московском часовом поясе (GMT+4).

-  *InvoiceAmendmentFlags* отражает статус данного ИКСФ: было ли затребовано уточнение, передавалось ли ИКСФ; представляет собой битовую маску, составленную из одного или нескольких значений перечисления *InvoiceAmendmentFlags*.

Перечисление *InvoiceStatus* задает возможные варианты состояний, в которых может находиться СФ/ИСФ/КСФ/ИКСФ:

-  *UnknownInvoiceStatus* (неизвестный статус; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать статус документа, переданный сервером),

-  *OutboundWaitingForInvoiceReceipt* (СФ/ИСФ/КСФ/ИКСФ исходящий, ожидается извещение о получении СФ/ИСФ/КСФ/ИКСФ от покупателя),

-  *OutboundNotFinished* (СФ/ИСФ/КСФ/ИКСФ исходящий, извещение о получении СФ/ИСФ/КСФ/ИКСФ от покупателя уже есть, но документооборот еще не завершен),

-  *OutboundFinished* (СФ/ИСФ/КСФ/ИКСФ исходящий, документооборот завершен),

-  *OutboundWaitingForSenderSignature* (СФ/ИСФ/КСФ/ИКСФ исходящий, документ не отправлен, поскольку не подписан отправителем),

-  *OutboundInvalidSenderSignature* (СФ/ИСФ/КСФ/ИКСФ исходящий, документ не отправлен, поскольку подпись отправителя не является корректной),

-  *InboundNotFinished* (СФ/ИСФ/КСФ/ИКСФ входящий, документооборот не завершен),

-  *InboundFinished* (СФ/ИСФ/КСФ/ИКСФ входящий, документооборот завершен).

Статус рассчитывается без учета уведомлений об уточнении и извещений об их получении.

Перечисление *InvoiceAmendmentFlags* задает возможные варианты статусов СФ/ИСФ/КСФ/ИКСФ с точки зрения наличия в Диадоке уведомления об уточнении или переданного исправления / корректировки:

-  *None* (уточнение не требуется, ИСФ/КСФ/ИКСФ не передавались),

-  *AmendmentRequested* (имеется уведомление об уточнении СФ/ИСФ/КСФ/ИКСФ),

-  *Revised* (СФ/ИСФ/КСФ/ИКСФ был исправлен, то есть было передано соответствующее ИСФ/ИКСФ),

-  *Corrected* (СФ/ИСФ был откорректирован, то есть был передан соответствующий КСФ).

Статус *Corrected* может быть присвоен только документам типа СФ/ИСФ.


