UniversalCorrectionDocumentSellerTitleInfo
==========================================

.. warning:: Эта структура использовалась в методах :doc:`../../http/utd/GenerateUniversalTransferDocumentXmlForSeller` и :doc:`../../http/utd/ParseUniversalCorrectionDocumentSellerTitleXml`, которые устарели с 1 октября 2021 года.

.. code-block:: protobuf
    :emphasize-lines: 1-20

    message UniversalCorrectionDocumentSellerTitleInfo {
        required FunctionType Function = 1;                          // Функция документа // Функция
        optional string DocumentName = 2;                            // Наименование первичного документа, определенное организацией // НаимДокОпр        
        required string DocumentDate  = 3;                           // дата УКД // ДатаКСчФ
        required string DocumentNumber  = 4;                         // номер УКД // НомерКСчФ
        repeated InvoiceForCorrectionInfo Invoices = 5;              // Счет-фактура (первичный документ), к которому составлен корректировочный счет-фактура // СчФ        
        required ExtendedOrganizationInfo Seller = 6;                // продавец // СвПрод
        required ExtendedOrganizationInfo Buyer = 7;                 // покупатель // СвПокуп
        repeated ExtendedSigner Signers = 8;                         // Подписант // Подписант
        required EventContent EventContent = 9;                      // Содержание события // СодФХЖ3
        required InvoiceCorrectionTable InvoiceCorrectionTable = 10; // Сведения таблицы корректировочного счета-фактуры // ТаблКСчФ
        required string Currency = 11;                               // валюта (код) // КодОКВ
        optional string CurrencyRate = 12;                           // Курс валюты // КурсВал
        optional string CorrectionRevisionDate = 13;                 // ДатаИспрКСчФ, обязателен, если формируется исправление // ДатаИспрКСчФ
        optional string CorrectionRevisionNumber = 14;               // НомИспрКСчФ, обязателен, если формируется исправление // НомИспрКСчФ
        optional AdditionalInfoId AdditionalInfoId = 15;             // информационное поле документа // ИнфПолФХЖ1
        required string DocumentCreator = 16;                        // Наименование экономического субъекта-составителя файла обмена счета-фактуры (информации продавца) // НаимЭконСубСост        
        optional string DocumentCreatorBase = 17;                    // Основание, по которому экономический субъект является составителем файла обмена счета-фактуры //ОснДоверОргСост        
        optional string GovernmentContractInfo = 18;                 // Идентификатор государственного контракта // ИдГосКон
    }

    message InvoiceForCorrectionInfo {
        required string InvoiceDate = 1;                             // ДатаСчФ
        required string InvoiceNumber = 2;                           // НомерСчФ
        repeated InvoiceRevisionInfo InvoiceRevisions = 3;           // С учетом исправления // ИспрСчФ
    }

    message InvoiceRevisionInfo {
        required string InvoiceRevisionDate = 1;                     // ДатаИспрСчФ (заполняется, если КСФ/ИКСФ формируется на исправленный СФ)
        required string InvoiceRevisionNumber = 2;                   // НомИспрСчФ (заполняется, если КСФ/ИКСФ формируется на исправленный СФ)
    }
 
    message EventContent {
        optional string CostChangeInfo = 1;                          // Иные сведения об изменении стоимости  // ИныеСвИзмСтоим
        optional string TransferDocDetails = 2;                      // Реквизиты передаточных документов, к которым относится корректировка // ПередатДокум
        required string OperationContent = 3;                        // Содержание операции // СодОпер
        optional string NotificationDate = 4;                        // Дата направления на согласование // ДатаНапр
        repeated CorrectionBase CorrectionBase = 5;                  // Основание корректировки // ОснКор
    }

    message CorrectionBase {
        required string BaseDocumentName = 1;                        // Наименование документа - основания // НаимОсн
        optional string BaseDocumentNumber = 2;                      // Номер документа - основания // НомОсн
        optional string BaseDocumentDate = 3;                        // Дата документа - основания, обязателен при НаимОсн отличном от значения "Отсутствует" // ДатаОсн
        optional string AdditionalInfo = 4;                          // Дополнительные сведения // ДопСвОсн
    }
  
    message InvoiceCorrectionTable {
        repeated ExtendedInvoiceCorrectionItem Items = 1;            // информация о товарах // СведТов
        optional InvoiceTotalsDiff TotalsInc = 2;                    // суммы к увеличению // ВсегоУвел
        optional InvoiceTotalsDiff TotalsDec = 3;                    // суммы к уменьшению // ВсегоУм
    }

    message ExtendedInvoiceCorrectionItem {
        required string Product = 1;                                 // наименование товара // НаимТов
        required CorrectableInvoiceItemFields OriginalValues = 2;    // значения до изменения
        required CorrectableInvoiceItemFields CorrectedValues = 3;   // значения после изменения
        optional InvoiceItemAmountsDiff AmountsInc = 4;              // суммы к увеличению
        optional InvoiceItemAmountsDiff AmountsDec = 5;              // суммы к уменьшению
        optional string ItemAccountDebit = 6;                        // Корреспондирующие счета: дебет // КорСчДебет
        optional string ItemAccountCredit = 7;                       // Корреспондирующие счета: кредит // КорСчКредит
        repeated AdditionalInfo AdditionalInfo = 8;                  // информационное поле документа // ИнфПолФХЖ2
    }

    message AdditionalInfoId {
        optional string InfoFileId = 1;             // Идентификатор файла информационного поля // ИдФайлИнфПол
        repeated AdditionalInfo AdditionalInfo = 2; //Текстовая информация // ТекстИнф
    }

    message AdditionalInfo {
        required string Id = 1;     // Идентификатор
        required string Value = 2;  // Значение
    }


Структура данных *UniversalCorrectionDocumentSellerTitleInfo* представляет исходные данные для формирования файлов в XML-формате при помощи метода :doc:`../../http/utd/GenerateUniversalTransferDocumentXmlForSeller` с параметром ``correction = true``.

При заполнении структуры *UniversalCorrectionDocumentSellerTitleInfo* нужно иметь в виду:

-  Первичные документы, к котором выставляются корректировочные документы заполняется в виде структуры *InvoiceForCorrectionInfo*,

-  Реквизиты продавца (*UniversalCorrectionDocumentSellerTitleInfo.Seller*) и покупателя (*UniversalCorrectionDocumentSellerTitleInfo.Buyer*) заполняются в виде структуры данных :doc:`ExtendedOrganizationInfo <ExtendedOrganizationInfo>`.

-  Реквизиты подписанта документа *UniversalCorrectionDocumentSellerTitleInfo.Signers* заполняются в виде структуры данных :doc:`ExtendedSigner`.

-  Даты документов должны указываться в формате ДД.ММ.ГГГГ.

-  Идентификатор файла информационного поля *AdditionalInfoId.InfoFileId* заполняется в формате GUID через дефис.

-  Если не указан код валюты *UniversalCorrectionDocumentSellerTitleInfo.Currency*, по умолчанию будет использоваться код 643 (Российский рубль).
