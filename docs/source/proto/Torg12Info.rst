Torg12Info
==========

.. code-block:: protobuf

    // титул продавца
    message Torg12SellerTitleInfo {
        required string DocumentDate = 1;                          // дата товарной накладной
        optional string DocumentNumber = 2;                        // номер товарной накладной
        required DocflowParticipant SellerDocflowParticipant = 3;  // участник документооборота, отпустивший товар
        required DocflowParticipant BuyerDocflowParticipant = 4;   // участник документооборота, которому отпущен товар
        optional OrganizationInfo Shipper = 5;                     // грузоотправитель
        optional OrganizationInfo Consignee = 6;                   // грузополучатель
        optional OrganizationInfo Supplier = 7;                    // поставщик
        optional OrganizationInfo Payer = 8;                       // плательщик
        optional Grounds Grounds = 9;                              // основание
        optional string WaybillDate = 10;                          // дата составления транспортной накладной
        optional string WaybillNumber = 11;                        // номер транспортной накладной
        optional string OperationCode = 12;                        // код вида операции
        repeated Torg12Item Items = 13;                            // табличные сведения товарной накладной
        optional string ParcelsQuantityTotal = 14;                 // количество мест, штук - всего по накладной
        optional string ParcelsQuantityTotalInWords = 15;          // количество мест, штук - всего по накладной, прописью
        optional string GrossQuantityTotal = 16;                   // брутто - всего по накладной
        optional string GrossQuantityTotalInWords = 17;            // брутто - всего по накладной, прописью
        optional string NetQuantityTotal = 18;                     // нетто - всего по накладной
        optional string NetQuantityTotalInWords = 19;              // нетто - всего по накладной, прописью
        optional string QuantityTotal = 20;                        // количество (масса нетто) - всего по накладной
        optional string TotalWithVatExcluded = 21;                 // сумма без учета НДС - всего по накладной
        optional string Vat = 22;                                  // сумма НДС - всего по накладной
        required string Total = 23;                                // сумма с учетом НДС - всего по накладной
        optional string TotalInWords = 24;                         // сумма с учетом НДС - всего по накладной, прописью
        optional string SupplyDate = 25;                           // дата отпуска
        optional Official SupplyAllowedBy = 26;                    // отпуск разрешил
        optional Official SupplyPerformedBy = 27;                  // отпуск произвел
        optional Official ChiefAccountant = 28;                    // главный бухгалтер
        required Signer Signer = 29;                               // подписант
        optional string AdditionalInfo = 30;                       // дополнительные сведения
        optional string AttachmentSheetsQuantity = 31;             // приложение, количество листов
    }

    message Torg12Item {
        required string Name = 1;                      // наименование
        optional string Feature = 2;                   // характеристика
        optional string Sort = 3;                      // сорт товара
        optional string NomenclatureArticle = 4;       // артикул
        optional string Code = 5;                      // код товара
        optional string UnitCode = 6;                  // код единицы измерения
        required string UnitName = 7;                  // наименование единицы измерения
        optional string ParcelType = 8;                // вид упаковки
        optional string ParcelCapacity = 9;            // количество в одном месте
        optional string ParcelsQuantity = 10;          // количество мест
        optional string GrossQuantity = 11;            // брутто
        required string Quantity = 12;                 // нетто // количество (масса)
        optional string Price = 13;                    // цена
        required string TaxRate = 14;                  // ставка налога
        optional string SubtotalWithVatExcluded = 15;  // сумма без учета налога
        optional string Vat = 16;                      // сумма налога
        required string Subtotal = 17;                 // сумма всего
        optional string AdditionalInfo = 18;           // информационное поле сведений о товаре
    }

    // документ-основание
    message Grounds {
        optional string DocumentName = 1;    // название документа
        optional string DocumentNumber = 2;  // номер документа
        optional string DocumentDate = 3;    // дата документа
        optional string AdditionalInfo = 4;  // дополнительные сведения
    }

    // титул покупателя
    message Torg12BuyerTitleInfo {
        required string ShipmentReceiptDate = 1;  // дата получения груза
        optional Attorney Attorney = 2;           // сведения по доверенности
        optional Official AcceptedBy = 3;         // лицо, принявшее груз
        optional Official ReceivedBy = 4;         // лицо, получившее груз
        required Signer Signer = 5;               // подписант
        optional string AdditionalInfo = 6;       // дополнительная информация
    }
        

Структура данных *Torg12SellerTitleInfo* представляет исходные данные для формирования титула продавца для товарной накладной в XML-формате при помощи метода :doc:`../http/GenerateTorg12XmlForSeller`.

При заполнении структуры *Torg12SellerTitleInfo* нужно иметь в виду:

-  Обязательные поля *Torg12SellerTitleInfo.SellerDocflowParticipant* и *Torg12SellerTitleInfo.BuyerDocflowParticipant* позволяют задать участников электронного обмена, между которыми происходит передача товарной накладной. Необходимая информация об участниках задается в виде структуры данных :doc:`DocflowParticipant <OrganizationInfo>`.

-  Реквизиты грузоотправителя *Torg12SellerTitleInfo.Shipper*, грузополучателя *Torg12SellerTitleInfo.Consignee*, поставщика *Torg12SellerTitleInfo.Supplier* и плательщика *Torg12SellerTitleInfo.Payer* заполняются в виде структуры данных :doc:`OrganizationInfo`.

-  Реквизиты подписанта накладной *Torg12SellerTitleInfo.Signer* заполняются в виде структуры данных :doc:`Signer`.

-  Реквизиты должностных лиц *Torg12SellerTitleInfo.SupplyAllowedBy*, *Torg12SellerTitleInfo.SupplyPerformedBy* и *Torg12SellerTitleInfo.ChiefAccountant* заполняются в виде структуры данных :doc:`Official`.

-  Правила заполнения структуры *Torg12SellerTitleInfo* повторяют требования формата ФНС, зафиксированные в следующей :download:`XML-схеме <../xsd/DP_OTORG12_1_986_00_05_01_02.xsd>`.

Структура данных *Torg12BuyerTitleInfo* представляет исходные данные для формирования титула продавца для товарной накладной в XML-формате при помощи метода :doc:`../http/GenerateTorg12XmlForBuyer`.

При заполнении структуры *Torg12BuyerTitleInfo* нужно иметь в виду:

-  Реквизиты подписанта накладной *Torg12BuyerTitleInfo.Signer* заполняются в виде структуры данных :doc:`Signer`.

-  Реквизиты должностных лиц *Torg12BuyerTitleInfo.AcceptedBy* и *Torg12BuyerTitleInfo.ReceivedBy* заполняются в виде структуры данных :doc:`Official`.

-  Реквизиты доверенности *Torg12BuyerTitleInfo.Attorney* заполняются в виде структуры данных :doc:`Attorney <Official>`.

-  Правила заполнения структуры *Torg12BuyerTitleInfo* повторяют требования формата ФНС, зафиксированные в следующей :download:`XML-схеме <../xsd/DP_PTORG12_1_989_00_05_01_02.xsd>`.