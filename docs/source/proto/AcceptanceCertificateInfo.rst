AcceptanceCertificateInfo
=========================

.. code-block:: protobuf

    // титул исполнителя
    message AcceptanceCertificateSellerTitleInfo {
        required DiadocOrganizationInfo Seller = 1;                 // исполнитель (продавец услуг)
        required DocflowParticipant Buyer = 2;                      // заказчик (покупатель услуг)
        required string DocumentDate = 3;                           // дата составления акта о выполнении
        optional string DocumentNumber = 4;                         // номер акта
        required string DocumentTitle = 5;                          // заголовок документа
        repeated WorkDescription Works = 6;                         // описание выполненных работ
        required AcceptanceCertificateSignatureInfo Signature = 7;  // сведения о подписи акта
        required Signer Signer = 8;                                 // подписант
        optional string AdditionalInfo = 9;                         // дополнительная информация
    }

    message WorkDescription {
        optional string StartingDate = 1;          // начало периода выполнения работ
        optional string CompletionDate = 2;        // окончание периода выполнения работ
        optional string TotalWithVatExcluded = 3;  // сумма без учета НДС - итого
        optional string Vat = 4;                   // сумма НДС - итого
        required string Total = 5;                 // сумма с учетом НДС - итого
        repeated WorkItem Items = 6;               // сведения о произведенной работе
    }

    message WorkItem {
        optional string Name = 1;                     // наименование
        optional string Description = 2;              // описание работы
        optional string UnitCode = 3;                 // код единицы измерения
        optional string UnitName = 4;                 // наименование единицы измерения
        optional string Price = 5;                    // цена
        optional string Quantity = 6;                 // количество
        optional string SubtotalWithVatExcluded = 7;  // сумма без учета НДС
        optional string Vat = 8;                      // сумма НДС
        optional string Subtotal = 9;                 // сумма с учетом НДС
        optional string AdditionalInfo = 10;          // информационное поле сведений о работе (услуге)
    }

    message AcceptanceCertificateSignatureInfo {
        optional string SignatureDate = 1;  // дата подписи акта исполнителем / заказчиком
        optional Official Official = 2;     // лицо, подписывающее со стороны исполнителя / заказчика
        optional Attorney Attorney = 3;     // сведения о доверенности подписывающего со стороны исполнителя / заказчика
    }

    // титул заказчика
    message AcceptanceCertificateBuyerTitleInfo {
        optional string Complaints = 1;                             // претензии
        required AcceptanceCertificateSignatureInfo Signature = 2;  // сведения о подписи акта
        required Signer Signer = 3;                                 // подписант
        optional string AdditionalInfo = 4;                         // дополнительная информация
    }
        

Структура данных *AcceptanceCertificateSellerTitleInfo* представляет исходные данные для формирования титула исполнителя для акта о выполнении работ/оказании услуг в XML-формате при помощи метода :doc:`../http/GenerateAcceptanceCertificateXmlForSeller`.

При заполнении структуры *AcceptanceCertificateSellerTitleInfo* нужно иметь в виду:

-  Реквизиты исполнителя (*AcceptanceCertificateSellerTitleInfo.Seller*) заполняются в виде структуры данных :doc:`DiadocOrganizationInfo <OrganizationInfo>`;

-  Реквизиты заказчика (*AcceptanceCertificateSellerTitleInfo.Buyer*) заполняются в виде структуры данных :doc:`DocflowParticipant <OrganizationInfo>`;

-  Реквизиты подписанта акта *AcceptanceCertificateSellerTitleInfo.Signer* заполняются в виде структуры данных :doc:`Signer`;

-  Правила заполнения структуры *AcceptanceCertificateSellerTitleInfo* повторяют требования формата ФНС, зафиксированные в следующей :download:`XML-схеме <../xsd/DP_IAKTPRM_1_987_00_05_01_02.xsd>`.

Структура данных *AcceptanceCertificateBuyerTitleInfo* представляет исходные данные для формирования титула заказчика для акта о выполнении работ/оказании услуг в XML-формате при помощи метода :doc:`../http/GenerateAcceptanceCertificateXmlForBuyer`.

При заполнении структуры *AcceptanceCertificateBuyerTitleInfo* нужно иметь в виду:

-  Реквизиты подписанта акта *AcceptanceCertificateBuyerTitleInfo.Signer* заполняются в виде структуры данных :doc:`Signer`.

-  Правила заполнения структуры *AcceptanceCertificateBuyerTitleInfo* повторяют требования формата ФНС, зафиксированные в следующей :download:`XML-схеме <../xsd/DP_ZAKTPRM_1_990_00_05_01_02.xsd>`.

Структура данных *AcceptanceCertificateSignatureInfo* представляет реквизиты подписи одной из сторон в акте:

-  *SignatureDate* - дата подписи в формате ДД.ММ.ГГГГ;

-  *Official* - информация о должностном лице, поставившем подпись; заполняются в виде структуры данных :doc:`Official`

-  *Attorney* - сведения о доверенности подписывающего со стороны исполнителя / заказчика; заполняются в виде структуры данных :doc:`Attorney <Official>`.
