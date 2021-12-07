UniversalTransferDocumentSellerTitleInfo
========================================

.. warning:: Эта структура использовалась в методах :doc:`../../http/utd/GenerateUniversalTransferDocumentXmlForSeller` и :doc:`../../http/utd/ParseUniversalTransferDocumentSellerTitleXml`, которые устарели с 1 октября 2021 года.

.. code-block:: protobuf
    :emphasize-lines: 1-22

    message UniversalTransferDocumentSellerTitleInfo {
        required FunctionType Function = 1;  // Функция документа // Функция
        optional string DocumentName = 2;    // Наименование первичного документа, определенное организацией // НаимДокОпр
        required string DocumentDate  = 3;   // дата УПД // ДатаСчФ
        required string DocumentNumber  = 4; // номер УПД // НомерСчФ
        required ExtendedOrganizationInfo Seller = 5;    // продавец // СвПрод
        required ExtendedOrganizationInfo Buyer = 6;     // покупатель //СвПокуп
        optional Shipper Shipper = 7;                                  // грузоотправитель //ГрузОт
        optional ExtendedOrganizationInfo Consignee = 8; // грузополучатель //ГрузПолуч
        repeated ExtendedSigner Signers = 9;        // подписант // Подписант
        repeated PaymentDocumentInfo PaymentDocuments = 10; // платежно-расчетные документы // СвПРД
        optional InvoiceTable InvoiceTable = 11;            // Сведения таблицы счета-фактуры // ТаблСчФакт
        required string Currency = 12;                      // валюта (код) // КодОКВ
        optional string CurrencyRate = 13;                  // Курс валюты // КурсВал
        optional string RevisionDate = 14;                  // дата ИСФ (обязательно при формировании UniversalTransferDocumentSellerTitleRevision) // ДатаИспрСчФ
        optional string RevisionNumber = 15;                // номер ИСФ (обязательно при формировании UniversalTransferDocumentSellerTitleRevision) // НомИспрСчФ
        optional AdditionalInfoId AdditionalInfoId = 16;    // информационное поле документа // ИнфПолФХЖ1
        optional TransferInfo TransferInfo = 17;            // Сведения о передаче (сдаче) // СвПродПер
        required string DocumentCreator = 18;               // Составитель файла обмена счета-фактуры (информации продавца) // НаимЭконСубСост
        optional string DocumentCreatorBase = 19;           // Основание, по которому экономический субъект является составителем файла обмена счета-фактуры //ОснДоверОргСост
        optional string GovernmentContractInfo = 20;         // ИдГосКон
    }

    enum FunctionType {
        Invoice = 0;         // СЧФ
        Basic = 1;           // ДОП
        InvoiceAndBasic = 2; // СЧФДОП
    }

    message Shipper {
        optional bool SameAsSeller = 1; // совпадает с продавцом // ОнЖе
        optional ExtendedOrganizationInfo OrgInfo = 2; // реквизиты организации // ГрузОтпр
    }


    message InvoiceTable {
        repeated ExtendedInvoiceItem Items = 1;   // информация о товарах // СведТов
        optional string TotalWithVatExcluded = 2; // Сумма без учета налога // СтТовБезНДСВсего
        required string Vat = 3;                  // Сумма налога // СумНалВсего
        required string Total = 4;                // Сумма всего // СтТовУчНалВсего
        optional string TotalNet = 5;             // Нетто всего // НеттоВс
    }

    message ExtendedInvoiceItem {
        required string Product = 1;  // наименование товара // НаимТов
        optional string Unit = 2;     // единицы измерения товара (код) // ОКЕИ_Тов
        optional string UnitName = 3; // наименование единицы измерения товара. Пользователь заполняет, если ОКЕИ_Тов=’0000’// НаимЕдИзм
        optional string Quantity = 4; // количество единиц товара // КолТов
        optional string Price = 5;    // цена за единицу товара // ЦенаТов
        optional string Excise = 6;   // акциз // СумАкциз
        required TaxRate TaxRate = 7; // ставка налога // НалСт
        optional string SubtotalWithVatExcluded = 8; // сумма без учета налога // СтТовБезНДС
        optional string Vat = 9;       // сумма налога // СумНал
        required string Subtotal = 10; // сумма всего // СтТовУчНал
        repeated CustomsDeclaration CustomsDeclarations = 11; // номера таможенных деклараций // СвТД
        optional ItemMark ItemMark = 12;             // Признак товар-работа-услуга // ПрТовРаб
        optional string AdditionalProperty = 13;     // Дополнительная информация о признаке //ДопПризн
        optional string ItemVendorCode = 14;         // Характеристика/код/артикул/сорт товара // КодТов
        optional string ItemToRelease = 15;          // Количество надлежит отпустить // НадлОтп
        optional string ItemAccountDebit = 16;       // Корреспондирующие счета: дебет // КорСчДебет
        optional string ItemAccountCredit = 17;      // Корреспондирующие счета: кредит // КорСчКредит
        repeated AdditionalInfo AdditionalInfo = 18; // информационное поле документа // ИнфПолФХЖ2
    }

    enum TaxRate {
        NoVat = 0;              //без НДС
        Percent_0 = 1;          //ставка налога 0%
        Percent_10 = 2;         //ставка налога 10%
        Percent_18 = 3;         //ставка налога 18%
        Percent_20 = 4;         //ставка налога 20%
        Fraction_10_110 = 5;    //ставка налога 10/110 (дробь)
        Fraction_18_118 = 6;    //ставка налога 18/118 (дробь)
        TaxedByAgent = 7;       //ставка налога "НДС исчисляется налоговым агентом"
        Fraction_20_120 = 8;    //ставка налога 20/120 (дробь)
    }

    enum ItemMark {
        NotSpecified = 0;   // не указано
        Property = 1;       // имущество
        Job = 2;            // работа
        Service = 3;        // услуга
        PropertyRights = 4; // имущественные права
        Other = 5;          // иное
    }

    message TransferInfo {
        required string OperationInfo = 1;               // Содержание операции // СодОпер
        optional string OperationType = 2;               // Вид операции // ВидОпер
        optional string TransferDate = 3;                // Дата отгрузки // ДатаПер
        repeated TransferBase TransferBase = 4;          // Основание отгрузки //ОснПер
        optional string TransferTextInfo = 5;            // Сведения о транспортировке и грузе // СвТранГруз
        repeated Waybill Waybill = 6;                    // Транспортная накладная //ТранНакл
        optional    ExtendedOrganizationInfo Carrier = 7; // Перевозчик // Перевозчик
        optional Employee Employee = 8;                  // Работник организации продавца //РабОргПрод
        optional OtherIssuer  OtherIssuer = 9;           // Иное лицо //ИнЛицо
        optional string CreatedThingTransferDate = 10;   // Дата передачи вещи, изготовленной по договору //ДатаПерВещ
        optional string CreatedThingInfo = 11;           // Сведения о передаче, изготовленной по договору //СвПерВещ
        optional AdditionalInfoId AdditionalInfoId = 12; // Информационное поле документа // ИнфПолФХЖ3
    }

    message TransferBase {
        required string BaseDocumentName = 1;   // Наименование документа-основания отгрузки //НаимОсн
        optional string BaseDocumentNumber = 2; // Номер документа-основания отгрузки //НомОсн
        optional string BaseDocumentDate = 3;   // Дата документа-основания отгрузки //ДатаОсн
        optional string BaseDocumentInfo = 4;   // Дополнительные сведения документа-основания отгрузки //ДопСвОсн
    }

    message  Waybill {
        required  string TransferDocumentNumber = 1; // Номер транспортной накладной // НомерТранНакл
        required  string TransferDocumentDate = 2;   // Дата транспортной накладной // ДатаТранНакл
    }

    message Employee {
        required string EmployeePosition = 1;   // Должность // Должность
        optional string EmployeeInfo = 2;       // Иные сведения, идентифицирующие физическое лицо // ИныеСвед
        optional string EmployeeBase = 3;       // Основание полномочий представителя // ОснПолн
        required string TransferSurname = 4;    // Фамилия //Фамилия
        required string TransferFirstName = 5;  // Имя //Имя
        optional string TransferPatronymic = 6; // Отчество //Отчество
    }

    message OtherIssuer {
        optional string TransferEmployeePosition = 1; // Должность представителя организации // Должность //если заполнено - формируется структура «ПредОргПер», если не заполнено – «ФЛПер»
        optional string TransferEmployeeInfo = 2;     // Иные сведения, идентифицирующие физическое лицо // ИныеСвед
        optional string TransferOrganizationName = 3; //Наименование организации, которой доверена передача // НаимОргПер
        optional string TransferOrganizationBase = 4; // Основание, по которому организации доверена передача // ОснДоверОргПер
        optional string TransferEmployeeBase = 5;     //Основание полномочий представителя // ОснПолнПредПер (ОснДоверФЛ)
        required string TransferSurname = 6;    //Фамилия //Фамилия
        required string TransferFirstName = 7;  //Имя //Имя
        optional string TransferPatronymic = 8; //Отчество //Отчество
    }

    message AdditionalInfoId {
        optional string InfoFileId = 1;             // Идентификатор файла информационного поля // ИдФайлИнфПол
        repeated AdditionalInfo AdditionalInfo = 2; //Текстовая информация // ТекстИнф
    }

    message AdditionalInfo {
        required string Id = 1;     // Идентификатор
        required string Value = 2;  // Значение
    }


Структура данных *UniversalTransferDocumentSellerTitleInfo* представляет исходные данные для формирования файлов в XML-формате при помощи метода :doc:`../../http/utd/GenerateUniversalTransferDocumentXmlForSeller`. При заполнении структуры UniversalTransferDocumentSellerTitleInfo нужно иметь в виду:

-  Реквизиты продавца (*UniversalTransferDocumentSellerTitleInfo.Seller*) и покупателя (*UniversalTransferDocumentSellerTitleInfo.Buyer*) заполняются в виде структуры данных :doc:`ExtendedOrganizationInfo <ExtendedOrganizationInfo>`.

-  Реквизиты грузоотправителя (*Shipper.OrgInfo*) заполняются в виде структуры данных :doc:`ExtendedOrganizationInfo <ExtendedOrganizationInfo>`. Если проставлен флаг *Shipper.SameAsSeller*, то реквизиты грузоотправителя заполнять не нужно - будут использоваться соответствующие реквизиты продавца.

-  Реквизиты грузополучателя (*UniversalTransferDocumentSellerTitleInfo.Consignee*) заполняются в виде структуры данных :doc:`ExtendedOrganizationInfo <ExtendedOrganizationInfo>`.

-  Реквизиты подписанта документа *UniversalTransferDocumentSellerTitleInfo.Signers* заполняются в виде структуры данных :doc:`ExtendedSigner`.

-  Даты документов должны указываться в формате ДД.ММ.ГГГГ.

-  Идентификатор файла информационного поля *AdditionalInfoId.InfoFileId* заполняется в формате GUID через дефис.

-  Суммы должны указываться в формате XXX.XX (дробная часть должна отделяться точкой). То же самое касается формата представления количества товара *ExtendedInvoiceItem.Quantity*.

-  Если не указан код валюты *UniversalTransferDocumentSellerTitleInfo.Currency*, по умолчанию будет использоваться код 643 (Российский рубль).

-  Коды единиц измерения *ExtendedInvoiceItem.Unit*, коды стран происхождения товара *InvoiceItem.CountriesOfOrigin*, а также коды иностранных государств *ForeignAddress.Country* можно указывать в буквенном формате, тогда Диадок предпримет попытку сконвертировать их в соответствующие числовые коды.
