AcceptanceCertificate552Info
============================

.. code-block:: protobuf

    message AcceptanceCertificate552SellerTitleInfo {
        required ExtendedOrganizationInfo Seller = 1;                     // Исполнитель (продавец услуг)
        required ExtendedOrganizationInfo Buyer = 2;                      // Заказчик (покупатель услуг)
        repeated ExtendedSigner Signers = 3;                              // Подписант
        repeated GroundInfo Grounds = 4;                                  // Основание
        required string Currency = 5;                                     // Валюта (код)
        optional string CurrencyRate = 6;                                 // Курс валюты
        repeated AcceptanceCertificate552WorkDescription Works = 7;       // описание выполненных работ
        required string DocumentDate = 8;                                 // Дата составления документа о передаче товара
        optional string DocumentNumber = 9;                               // Номер документа о передаче товара
        optional string RevisionDate = 10;                                // Дата исправления документа
        optional string RevisionNumber = 11;                              // Номер исправления документа
        required string DocumentCreator = 12;                             // Составитель файла информации продавца
        optional string DocumentCreatorBase = 13;                         // Основание, по которому экономический субъект является составителем файла
        optional string OperationType = 14;                               // Вид операции
        optional string OperationTitle = 15;                              // Заголовок содержания операции
        optional string GovernmentContractInfo = 16;                      // Идентификатор государственного контракта
        optional AdditionalInfoId AdditionalInfoId = 17;                  // Информационное поле документа
        required string DocumentName = 18;                                // Наименование первичного документа, определенное организацией
        required AcceptanceCertificate552TransferInfo TransferInfo = 19;  // Содержание факта хозяйственной жизни - сведения о передаче результатов работ (о предъявлении оказанных услуг)
    }

    message AcceptanceCertificate552TransferInfo {
        required string OperationInfo = 1;             // Содержание операции
        optional string TransferDate = 2;              // Дата передачи результатов работ
        optional string CreatedThingTransferDate = 3;  // Дата передачи вещи, изготовленной по договору подряда
        optional string CreatedThingInfo = 4;          // Сведения о передаче
        repeated AdditionalInfo AdditionalInfos = 5;   // Информационное поле документа
    }

    message AcceptanceCertificate552WorkDescription {
        optional string StartingDate = 1;                     // начало периода выполнения работ
        optional string CompletionDate = 2;                   // окончание периода выполнения работ
        optional string TotalWithVatExcluded = 3;             // сумма без учета НДС - итого
        optional string TotalVat = 4;                         // сумма НДС - итого
        required string Total = 5;                            // сумма с учетом НДС - итого
        repeated AcceptanceCertificate552WorkItem Items = 6;  // сведения о произведенной работе
    }

    message AcceptanceCertificate552WorkItem {
        optional string Name = 1;                              // наименование
        optional string Description = 2;                       // описание работы
        optional string UnitCode = 3;                          // код единицы измерения
        optional string UnitName = 4;                          // наименование единицы измерения
        optional string Price = 5;                             // цена
        optional string Quantity = 6;                          // количество
        optional string SubtotalWithVatExcluded = 7;           // сумма без учета НДС
        optional string Vat = 8;                               // сумма НДС
        optional string Subtotal = 9;                          // сумма с учетом НДС
        repeated AdditionalInfo AdditionalInfos = 10;          // информационное поле сведений о работе (услуге)
        optional TaxRate TaxRate = 11 [default = Percent_18];  // ставка налога
        optional string ItemAccountDebit = 12;                 // Корреспондирующие счета: дебет
        optional string ItemAccountCredit = 13;                // Корреспондирующие счета: кредит
    }

    message AcceptanceCertificate552BuyerTitleInfo {
        repeated ExtendedSigner Signers = 1;              // Подписант
        required string DocumentCreator = 2;              // Составитель файла информации продавца
        optional string DocumentCreatorBase = 3;          // Основание, по которому экономический субъект является составителем файла
        optional string OperationType = 4;                // Вид операции
        required string DocumentName = 5;                 // Наименование первичного документа, определенное организацией
        required string OperationContent = 6;                // Содержание операции
        optional string AcceptanceDate = 7;                   // Дата приемки результатов работ
        optional string CreatedThingAcceptDate = 8;       // Дата получения вещи, изготовленной  по договору подряда
        optional string CreatedThingInfo = 9;             // Сведения о получении
        optional AdditionalInfoId AdditionalInfoId = 10;  // Информационное поле документа
    }

Структура данных *AcceptanceCertificate552SellerTitleInfo* представляет исходные данные для формирования титула продавца для товарной накладной в XML-формате при помощи метода :doc:`../http/GenerateAcceptanceCertificateXmlForSeller` с параметром `documentVersion=rezru_05_01_01`.

При заполнении структуры *AcceptanceCertificate552SellerTitleInfo* нужно иметь в виду:

-  Обязательные поля *AcceptanceCertificate552SellerTitleInfo.Seller* и *AcceptanceCertificate552SellerTitleInfo.Buyer* позволяют задать участников электронного обмена, между которыми происходит передача товарной накладной. Необходимая информация об участниках задается в виде структуры данных :doc:`ExtendedOrganizationInfo <utd/ExtendedOrganizationInfo>`.

-  Основания задаются в виде структуры данных :doc:`GroundInfo <TovTorgInfo>`.

-  Реквизиты подписантов накладной *AcceptanceCertificate552SellerTitleInfo.Signers* заполняются в виде структуры данных :doc:`utd/ExtendedSigner`.

-  Правила заполнения структуры *AcceptanceCertificate552SellerTitleInfo* повторяют требования формата ФНС, зафиксированные в следующей :download:`XML-схеме <../xsd/DP_REZRUISP_1_990_01_05_01_02.xsd>`.

Структура данных *AcceptanceCertificate552BuyerInfo* представляет исходные данные для формирования титула продавца для товарной накладной в XML-формате при помощи метода :doc:`../http/GenerateAcceptanceCertificateXmlForBuyer` с параметром `documentVersion=rezru_05_01_01`.

При заполнении структуры *AcceptanceCertificate552BuyerInfo* нужно иметь в виду:

-  Реквизиты подписантов накладной *AcceptanceCertificate552BuyerInfo.Signers* заполняются в виде структуры данных :doc:`utd/ExtendedSigner`.

-  Правила заполнения структуры *AcceptanceCertificate552BuyerInfo* повторяют требования формата ФНС, зафиксированные в следующей :download:`XML-схеме <../xsd/DP_REZRUZAK_1_990_02_05_01_01.xsd>`.
