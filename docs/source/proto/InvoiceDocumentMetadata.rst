InvoiceDocumentMetadata
=======================

.. code-block:: protobuf

    message InvoiceMetadata {
        optional InvoiceStatus InvoiceStatus = 1 [default = UnknownInvoiceStatus];
        required string Total = 2;
        required string Vat = 3;
        required int32 Currency = 4;
        required sfixed64 ConfirmationDateTimeTicks = 5;
        required int32 InvoiceAmendmentFlags = 6;
    }

    message InvoiceRevisionMetadata {
        optional InvoiceStatus InvoiceRevisionStatus = 1 [default = UnknownInvoiceStatus];
        required string OriginalInvoiceNumber = 2;
        required string OriginalInvoiceDate = 3;
        required string Total = 4;
        required string Vat = 5;
        required int32 Currency = 6;
        required sfixed64 ConfirmationDateTimeTicks = 7;
        required int32 InvoiceAmendmentFlags = 8;
    }

    message InvoiceCorrectionMetadata {
        optional InvoiceStatus InvoiceCorrectionStatus = 1 [default = UnknownInvoiceStatus];
        required string OriginalInvoiceNumber = 2;
        required string OriginalInvoiceDate = 3;
        optional string OriginalInvoiceRevisionNumber = 4;
        optional string OriginalInvoiceRevisionDate = 5;
        required string TotalInc = 6;
        required string TotalDec = 7;
        required string VatInc = 8;
        required string VatDec = 9;
        required int32 Currency = 10;
        required sfixed64 ConfirmationDateTimeTicks = 11;
        required int32 InvoiceAmendmentFlags = 12;
    }

    message InvoiceCorrectionRevisionMetadata {
        optional InvoiceStatus InvoiceCorrectionRevisionStatus = 1 [default = UnknownInvoiceStatus];
        required string OriginalInvoiceNumber = 2;
        required string OriginalInvoiceDate = 3;
        optional string OriginalInvoiceRevisionNumber = 4;
        optional string OriginalInvoiceRevisionDate = 5;
        required string OriginalInvoiceCorrectionNumber = 6;
        required string OriginalInvoiceCorrectionDate = 7;
        required string TotalInc = 8;
        required string TotalDec = 9;
        required string VatInc = 10;
        required string VatDec = 11;
        required int32 Currency = 12;
        required sfixed64 ConfirmationDateTimeTicks = 13;
        required int32 InvoiceAmendmentFlags = 14;
    }

    enum InvoiceStatus {
        UnknownInvoiceStatus = 0;
        OutboundWaitingForInvoiceReceipt = 1;
        OutboundNotFinished = 2;
        OutboundFinished = 3;
        OutboundWaitingForSenderSignature = 6;
        OutboundInvalidSenderSignature = 7;
        InboundNotFinished = 4;
        InboundFinished = 5;
    }

Структура данных *InvoiceMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`Document`) специфичные для счетов-фактур:

-  *InvoiceStatus* определяет состояние, в котором находится документооборот по данному СФ; принимает одно из значений перечисления *InvoiceStatus*.

-  *Total* - сумма счета-фактуры (берется из самого файла СФ).

-  *Vat* - сумма НДС счета-фактуры (берется из самого файла СФ).

-  *Currency* - код валюты счета-фактуры (берется из самого файла СФ).

-  *ConfirmationDateTimeTicks* - метка времени подтверждения оператора ДО об отправке исходящего СФ или о доставке входящего СФ. Представляет собой целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001. Данная метка представляет момент времени в московском часовом поясе (GMT+4).

-  :doc:`InvoiceAmendmentFlags` отражает статус данного СФ: было ли затребовано уточнение, передавалось ли ИСФ, передавался ли КСФ;
   представляет собой битовую маску, составленную из одного или нескольких значений перечисления :doc:`InvoiceAmendmentFlags`.

Структура данных *InvoiceRevisionMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`Document`) специфичные для исправлений счетов-фактур:

-  *InvoiceRevisionStatus* определяет состояние, в котором находится документооборот по данному ИСФ; принимает одно из значений перечисления *InvoiceStatus*.

-  *OriginalInvoiceNumber* - номер исходного счета-фактуры (берется из самого файла ИСФ).

-  *OriginalInvoiceDate* - дата исходного счета-фактуры в формате ДД.ММ.ГГГГ (берется из самого файла ИСФ).

-  *Total* - сумма исправления счета-фактуры (берется из самого файла ИСФ).

-  *Vat* - сумма НДС исправления счета-фактуры (берется из самого файла ИСФ).

-  *Currency* - код валюты исправления счета-фактуры (берется из самого файла ИСФ).

-  *ConfirmationDateTimeTicks* - метка времени подтверждения оператора ДО об отправке исходящего ИСФ или о доставке входящего ИСФ.
   Представляет собой целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001. Данная метка представляет момент времени в московском часовом поясе (GMT+4).

-  :doc:`InvoiceAmendmentFlags` отражает статус данного ИСФ: было ли затребовано уточнение, передавалось ли ИСФ, передавался ли КСФ;
   представляет собой битовую маску, составленную из одного или нескольких значений перечисления :doc:`InvoiceAmendmentFlags`.

Структура данных *InvoiceCorrectionMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`Document`) специфичные для корректировочных счетов-фактур:

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

-  :doc:`InvoiceAmendmentFlags` отражает статус данного КСФ: было ли затребовано уточнение, передавалось ли ИКСФ; представляет собой битовую маску, составленную из одного или нескольких значений перечисления :doc:`InvoiceAmendmentFlags`.

Структура данных *InvoiceCorrectionRevisionMetadata* содержит дополнительные атрибуты документа (в структуре :doc:`Document`) специфичные для исправлений корректировочных счетов-фактур:

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

-  :doc:`InvoiceAmendmentFlags` отражает статус данного ИКСФ: было ли затребовано уточнение, передавалось ли ИКСФ; представляет собой битовую маску, составленную из одного или нескольких значений перечисления :doc:`InvoiceAmendmentFlags`.

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

