InvoiceInfo
===========

.. code-block:: protobuf

    message InvoiceInfo {
        required string InvoiceDate = 1;                    // дата СФ
        required string InvoiceNumber = 2;                  // номер СФ
        required DiadocOrganizationInfo Seller = 3;         // продавец
        required DiadocOrganizationInfo Buyer = 4;          // покупатель
        optional ShipperOrConsignee Shipper = 5;            // грузоотправитель
        optional ShipperOrConsignee Consignee = 6;          // грузополучатель
        required Signer Signer = 7;                         // подписант
        repeated PaymentDocumentInfo PaymentDocuments = 8;  // платежно-расчетные документы
        repeated InvoiceItem Items = 9;                     // информация о товарах
        optional string Currency = 10;                      // валюта (код)
        optional string TotalWithVatExcluded = 11;          // сумма без учета налога
        optional string Vat = 12;                           // сумма налога
        required string Total = 13;                         // сумма всего
        optional string AdditionalInfo = 14;                // информационное поле документа v5.01
        optional string InvoiceRevisionDate = 15;           // дата ИСФ (обязательно при формировании InvoiceRevision)
        optional string InvoiceRevisionNumber = 16;         // номер ИСФ (обязательно при формировании InvoiceRevision)
        repeated AdditionalInfo AdditionalInfos = 17;       // информационное поле документа v5.02
        optional InvoiceFormatVersion Version = 18 [default = DefaultInvoiceFormatVersion]; // версия формата ФУФа (для тестирования систем в переходном периоде)
    }

    message AdditionalInfo {
        required string Id = 1;     // Идентификатор
        required string Value = 2;  // Значение
    }

    enum InvoiceFormatVersion {
        DefaultInvoiceFormatVersion = 0;
        v5_01 = 1;
        v5_02 = 2;
    }

    message InvoiceItem {
        required string Product = 1;                    // наименование товара
        optional string Unit = 2;                       // единицы измерения товара (код)
        optional string Quantity = 3;                   // количество единиц товара
        optional string Price = 4;                      // цена за единицу товара
        repeated string CountriesOfOrigin = 5;          // страны происхождения товара (коды)
        repeated string CustomsDeclarationNumbers = 6;  // номера таможенных деклараций v5.01
        optional string Excise = 7;                     // акциз
        required TaxRate TaxRate = 8;                   // ставка налога
        optional string SubtotalWithVatExcluded = 9;    // сумма без учета налога
        optional string Vat = 10;                       // сумма налога
        required string Subtotal = 11;                  // сумма всего
        optional string AdditionalInfo = 12;            // информационное поле товара v5.01
        repeated CustomsDeclaration CustomsDeclarations = 13; // номера таможенных деклараций v5.02
        repeated AdditionalInfo AdditionalInfos = 14;   // информационное поле товара v5.02
    }

    message CustomsDeclaration {
        required string CountryCode = 1;                // код страны происхождения товара
        required string DeclarationNumber = 2;          // номер таможенной декларации
    }

    enum TaxRate {
        NoVat = 0;            //без НДС
        Percent_0 = 1;        //ставка налога 0%
        Percent_10 = 2;       //ставка налога 10%
        Percent_18 = 3;       //ставка налога 18%
        Percent_20 = 4;       //ставка налога 20%
        Fraction_10_110 = 5;  //ставка налога 10/110 (дробь)
        Fraction_18_118 = 6;  //ставка налога 18/118 (дробь)
        TaxedByAgent = 7;     //ставка налога "НДС исчисляется налоговым агентом"
        Fraction_20_120 = 8;  //ставка налога 20/120 (дробь)
    }

    message PaymentDocumentInfo {
        required string DocumentDate = 1;
        required string DocumentNumber = 2;
    }

    message ShipperOrConsignee {
        optional bool SameAsSellerOrBuyer = 1;  //совпадает с продавцом/покупателем
        optional OrganizationInfo OrgInfo = 2;  //реквизиты организации
    }
        

Структура данных *InvoiceInfo* представляет исходные данные для формирования счета-фактуры в XML-формате при помощи метода :doc:`../http/GenerateInvoiceXml`. При заполнении структуры InvoiceInfo нужно иметь в виду:

-  Реквизиты продавца (*InvoiceInfo.Seller*) и покупателя (*InvoiceInfo.Buyer*) заполняются в виде структуры данных :doc:`DiadocOrganizationInfo <OrganizationInfo>`.

-  Реквизиты грузоотправителя и грузополучателя (*ShipperOrConsignee.OrgInfo*) заполняются в виде структуры данных :doc:`OrganizationInfo <OrganizationInfo>`. Если проставлен флаг *ShipperOrConsignee.SameAsSellerOrBuyer*, то реквизиты грузоотправителя/грузополучателя заполнять не нужно - будут использоваться соответствующие реквизиты продавца/покупателя.

-  Реквизиты подписанта счета-фактуры *InvoiceInfo.Signer* заполняются в виде структуры данных :doc:`Signer`.

-  Даты документов должны указываться в формате ДД.ММ.ГГГГ.

-  Суммы должны указываться в формате XXX.XX (дробная часть должна отделяться точкой). То же самое касается формата представления количества товара *InvoiceItem.Quantity*.

-  Если не указан код валюты *InvoiceInfo.Currency*, по умолчанию будет использоваться код 643 (Российский рубль). Код валюты можно указывать в буквенном формате (например, "USD" - Доллар США), тогда он будет автоматически сконвертирован в соответствующий числовой код.

-  Коды единиц измерения *InvoiceItem.Unit*, коды стран происхождения товара *InvoiceItem.CountriesOfOrigin*, а также коды иностранных госудраств *ForeignAddress.Country* можно указывать в буквенном формате, тогда Диадок предпримет попытку сконвертироваить их в соответствующие числовые коды.

-  Версия формата счета-фактуры по умолчанию *DefaultInvoiceFormatVersion* до 14.04.2015 будет v5_01, после 14.04.2015 будет v5_02

-  В зависимости от значения поля InvoiceFormatVersion, из сериализованной структуры :doc:`InvoiceInfo` обрабатываются поля, соответствующие указанной версии (указаны в комментариях к полям).

-  Правила заполнения структуры InvoiceInfo повторяют требования формата ФНС, зафиксированные в следующей :download:`XML-схеме, v5.02 <../xsd/ON_SFAKT_1_897_01_05_02_02.xsd>`.
