InvoiceCorrectionInfo
=====================

.. code-block:: protobuf

    message InvoiceCorrectionInfo {
        required string InvoiceDate = 1;                      // дата СФ
        required string InvoiceNumber = 2;                    // номер СФ
        optional string InvoiceRevisionDate = 3;              // дата ИСФ (заполняется, если КСФ/ИКСФ формируется на исправленный СФ)
        optional string InvoiceRevisionNumber = 4;            // номер ИСФ (заполняется, если КСФ/ИКСФ формируется на исправленный СФ)
        required string InvoiceCorrectionDate = 5;            // дата КСФ
        required string InvoiceCorrectionNumber = 6;          // номер КСФ
        optional string InvoiceCorrectionRevisionDate = 7;    // дата ИКСФ (обязательно при формировании InvoiceCorrectionRevision)
        optional string InvoiceCorrectionRevisionNumber = 8;  // номер ИКСФ (обязательно при формировании InvoiceCorrectionRevision)
        required DiadocOrganizationInfo Seller = 9;           // продавец
        required DiadocOrganizationInfo Buyer = 10;           // покупатель
        required Signer Signer = 11;                          // подписант
        repeated InvoiceCorrectionItem Items = 12;            // информация о товарах
        optional string Currency = 13;                        // валюта (код)
        optional InvoiceTotalsDiff TotalsInc = 14;            // суммы к увеличению
        optional InvoiceTotalsDiff TotalsDec = 15;            // суммы к уменьшению
        optional string AdditionalInfo = 16;                  // информационное поле документа v5.01
        repeated AdditionalInfo AdditionalInfos = 17;         // информационное поле документа v5.02
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

    message InvoiceTotalsDiff {
        optional string TotalWithVatExcluded = 1;  // сумма без учета налога
        optional string Vat = 2;                   // сумма налога
        required string Total = 3;                 // сумма всего
    }

    message InvoiceCorrectionItem {
        required string Product = 1;                                // наименование товара
        required CorrectableInvoiceItemFields OriginalValues = 2;   // значения до изменения
        required CorrectableInvoiceItemFields CorrectedValues = 3;  // значения после изменения
        optional InvoiceItemAmountsDiff AmountsInc = 4;             // суммы к увеличению
        optional InvoiceItemAmountsDiff AmountsDec = 5;             // суммы к уменьшению
        optional string AdditionalInfo = 6;                         // информационное поле товара v5.01
        repeated AdditionalInfo AdditionalInfos = 7;                // информационное поле товара v5.02
    }

    message CorrectableInvoiceItemFields {
        optional string Unit = 1;                     // единицы измерения товара (код)
        optional string Quantity = 2;                 // количество единиц товара
        optional string Price = 3;                    // цена за единицу товара
        optional string Excise = 4;                   // акциз
        required TaxRate TaxRate = 5;                 // ставка налога
        optional string SubtotalWithVatExcluded = 6;  // сумма без учета налога
        optional string Vat = 7;                      // сумма налога
        required string Subtotal = 8;                 // сумма с учетом налога
    }

    message InvoiceItemAmountsDiff {
        optional string Excise = 1;                   // акциз
        optional string SubtotalWithVatExcluded = 2;  // сумма без учета налога
        optional string Vat = 3;                      // сумма налога
        optional string Subtotal = 4;                 // сумма с учетом налога
    }
        

Структура данных InvoiceCorrectionInfo представляет исходные данные для формирования корректировочного счета-фактуры в XML-формате при помощи метода :doc:`../http/GenerateInvoiceXml`. При заполнении структуры InvoiceCorrectionInfo нужно иметь в виду:

-  Реквизиты продавца (InvoiceCorrectionInfo.Seller) и покупателя (InvoiceCorrectionInfo.Buyer) заполняются в виде структуры данных :doc:`DiadocOrganizationInfo <OrganizationInfo>`.

-  Реквизиты подписанта счета-фактуры InvoiceCorrectionInfo.Signer заполняются в виде структуры данных :doc:`Signer`.

-  Даты документов должны указываться в формате ДД.ММ.ГГГГ.

-  Суммы должны указываться в формате XXX.XX (дробная часть должна отделяться точкой). То же самое касается формата представления количества товара CorrectableInvoiceItemFields.Quantity.

-  Если не указан код валюты InvoiceCorrectionInfo.Currency, по умолчанию будет использоваться код 643 (Российский рубль). Код валюты можно указывать в буквенном формате (например, "USD" - Доллар США), тогда он будет автоматически сконвертирован в соответствующий числовой код.

-  Коды единиц измерения CorrectableInvoiceItemFields.Unit, а также коды иностранных госудраств ForeignAddress.Country можно указывать в буквенном формате, тогда Диадок предпримет попытку сконвертироваить их в соответствующие числовые коды.

-  Версия формата корректировочного счета-фактуры по умолчанию DefaultInvoiceFormatVersion до 14.04.2015 будет v5_01, после 14.04.2015 будет v5_02

-  В зависимости от значения поля InvoiceFormatVersion, из сериализованной структуры :doc:`InvoiceCorrectionInfo`  обрабатываются поля, соответствующие указанной версии (указаны в комментариях к полям).

-  Правила заполнения структуры InvoiceCorrectionInfo повторяют требования формата ФНС, зафиксированные в следующей :download:`XML-схеме, v5.02 <../xsd/ON_KORSFAKT_1_911_01_05_02_02.xsd>`.
