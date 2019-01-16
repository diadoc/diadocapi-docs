TovTorgInfo
===========


.. code-block:: protobuf

    message TovTorgSellerTitleInfo {
        required ExtendedOrganizationInfo Seller = 1;     // Продавец
        required ExtendedOrganizationInfo Buyer = 2;      // Покупатель
        optional ExtendedOrganizationInfo Shipper = 3;    // Грузоотправитель
        optional ExtendedOrganizationInfo Consignee = 4;  // Грузополучатель
        optional ExtendedOrganizationInfo Carrier = 5;    // Перевозчик
        repeated ExtendedSigner Signers = 6;              // Подписант
        repeated GroundInfo Grounds = 7;                  // Основание
        required string Currency = 8;                     // Валюта (код)
        optional string CurrencyRate = 9;                 // Курс валюты
        required string DocumentDate = 10;                // Дата составления документа о передаче товара
        optional string DocumentNumber = 11;              // Номер документа о передаче товара
        optional string RevisionDate = 12;                // Дата исправления документа о передаче товара
        optional string RevisionNumber = 13;              // Номер исправления документа о передаче товара
        required TovTorgTransferInfo TransferInfo = 14;   // Сведения о факте передачи (об отпуске груза)
        required string DocumentCreator = 15;             // Составитель файла информации продавца
        optional string DocumentCreatorBase = 16;         // Основание, по которому экономический субъект является составителем файла
        optional string OperationType = 17;               // Вид операции
        optional string GovernmentContractInfo = 18;      // Идентификатор государственного контракта
        optional TovTorgTable Table = 19;                 // Сведения об ассортименте, количестве, стоимости и другой информации о товарных позициях
        optional AdditionalInfoId AdditionalInfoId = 20;  // Информационное поле документа
        required string DocumentName = 21;                // Наименование первичного документа, определенное организацией
    }

    message TovTorgBuyerTitleInfo {
        required string DocumentCreator = 1;             // Наименование экономического субъекта - составителя файла обмена информации покупателя
        optional string DocumentCreatorBase = 2;         // Основание, по которому экономический субъект является составителем файла обмена информации покупателя
        optional string OperationCode = 3;               // Вид операции
        required string OperationContent = 4;            // Содержание операции
        optional string AcceptanceDate = 5;              // Дата принятия товаров (результатов выполненных работ), имущественных прав (подтверждения факта оказания услуг)
        optional Employee Employee = 6;                  // работник организации покупателя
        optional OtherIssuer OtherIssuer = 7;            // Иное Лицо
        optional AdditionalInfoId AdditionalInfoId = 8;  // Информационное поле факта хозяйственной жизни (4)
        repeated ExtendedSigner Signers = 9;             // Подписант
    }

    message TovTorgTable {
        repeated TovTorgItem Items = 1;            // информация о товарах
        optional string TotalQuantity = 2;         // Количество мест всего по документу
        optional string TotalGross = 3;            // Масса брутто всего по документу
        optional string TotalNet = 4;              // Масса нетто всего по документу
        optional string TotalWithVatExcluded = 5;  // Сумма без учета налога
        optional string TotalVat = 6;              // Сумма НДС - всего по документу
        optional string Total = 7;                 // Сумма всего
    }

    message TovTorgItem {
        optional string Product = 1;                           // наименование товара
        optional string Feature = 2;                           // характеристика товара
        optional string Sort = 3;                              // сорт товара
        optional string VendorCode = 4;                        // арти
        optional string ProductCode = 5;                       // Код товара
        optional string UnitName = 6;                          // наименование единицы измерения товара. Пользователь заполняет, если ОКЕИ_Тов=’0000
        required string Unit = 7;                              // единицы измерения товара (код)
        optional string PackageType = 8;                       // вид упаковки товара
        optional string QuantityInPack = 9;                    // количество мест в 1 упаковке
        optional string Quantity = 10;                         // количество единиц товара
        optional string Gross = 11;                            // масса брутто
        required string Net = 12;                              // масса нетто, количество передано (отпущено)
        optional string ItemToRelease = 13;                    // Количество надлежит отпустить
        optional string Price = 14;                            // цена за единицу товара
        optional string SubtotalWithVatExcluded = 15;          // сумма без учета налога
        optional TaxRate TaxRate = 16 [default = Percent_18];  // ставка налога
        optional string Vat = 17;                              // сумма налога
        required string Subtotal = 18;                         // сумма всего
        optional string ItemAccountDebit = 19;                 // Корреспондирующие счета: дебет
        optional string ItemAccountCredit = 20;                // Корреспондирующие счета: кредит
        repeated AdditionalInfo AdditionalInfos = 21;          // Информационное поле документа
    }

    message TovTorgTransferInfo {
        required string OperationInfo = 1;            // Содержание операции
        optional string TransferDate = 2;             // Дата отгрузки
        optional string Attachment = 3;               // Приложение, сертификаты и прочее
        repeated Waybill Waybills = 4;                // Транспортная накладная
        optional Employee Employee = 5;               // Работник организации продавца
        optional OtherIssuer OtherIssuer = 6;         // Иное лицо
        repeated AdditionalInfo AdditionalInfos = 7;  // Информационное поле документа
    }

    message GroundInfo {
        required string Name = 1;    // Наименование документа - основания
        optional string Number = 2;  // Номер документа - основания
        optional string Date = 3;    // Дата документа - основания
        optional string Info = 4;    // Дополнительные сведения
    }


Структура данных *TovTorgSellerTitleInfo* представляет исходные данные для формирования титула продавца для товарной накладной в XML-формате при помощи метода :doc:`../http/GenerateTorg12XmlForSeller` с параметром `documentVersion=tovtorg_05_01_02`.

При заполнении структуры *TovTorgSellerTitleInfo* нужно иметь в виду:

-  Обязательные поля *TovTorgSellerTitleInfo.Seller* и *TovTorgSellerTitleInfo.Buyer* позволяют задать участников электронного обмена, между которыми происходит передача товарной накладной. Необходимая информация об участниках задается в виде структуры данных :doc:`ExtendedOrganizationInfo <utd/ExtendedOrganizationInfo>`.

-  Реквизиты грузоотправителя *TovTorgSellerTitleInfo.Shipper*, грузополучателя *TovTorgSellerTitleInfo.Consignee* и перевозчика *TovTorgSellerTitleInfo.Carrier* заполняются в виде структуры данных :doc:`utd/ExtendedOrganizationInfo`.

-  Реквизиты подписантов накладной *TovTorgSellerTitleInfo.Signers* заполняются в виде структуры данных :doc:`utd/ExtendedSigner`.

-  Правила заполнения структуры *TovTorgSellerTitleInfo* повторяют требования формата ФНС, зафиксированные в следующей :download:`XML-схеме <../xsd/DP_TOVTORGPR_1_992_01_05_01_04.xsd>`.

Структура данных *TovTorgBuyerTitleInfo* представляет исходные данные для формирования титула продавца для товарной накладной в XML-формате при помощи метода :doc:`../http/GenerateTorg12XmlForBuyer` с параметром `documentVersion=tovtorg_05_01_02`.

При заполнении структуры *TovTorgBuyerTitleInfo* нужно иметь в виду:

-  Реквизиты подписантов накладной *TovTorgBuyerTitleInfo.Signers* заполняются в виде структуры данных :doc:`utd/ExtendedSigner`.

-  Реквизиты должностных лиц *TovTorgBuyerTitleInfo.Employee* или *TovTorgBuyerTitleInfo.OtherIssuer* заполняются в виде структуры данных :doc:`Employee <utd/UniversalTransferDocumentSellerTitleInfo>` или :doc:`OtherIssuer <utd/UniversalTransferDocumentSellerTitleInfo>` соответственно.

-  Правила заполнения структуры *TovTorgBuyerTitleInfo* повторяют требования формата ФНС, зафиксированные в следующей :download:`XML-схеме <../xsd/DP_TOVTORGPOK_1_992_02_05_01_04.xsd>`.
