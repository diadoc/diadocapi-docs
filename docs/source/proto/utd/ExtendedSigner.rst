ExtendedSigner
==============

.. code-block:: protobuf
    :emphasize-lines: 1-6

    message ExtendedSigner {
        optional string BoxId = 1;
        optional bytes SignerCertificate = 2;
        optional string SignerCertificateThumbprint = 3;
        optional ExtendedSignerDetails SignerDetails = 4;
    }

    message ExtendedSignerDetails {
        required string Surname = 1;
        required string FirstName = 2;
        optional string Patronymic = 3;
        optional string JobTitle = 4;
        optional string Inn = 5;
        optional string RegistrationCertificate = 6;

        required SignerType SignerType = 7 [default = LegalEntity]; // Физическое лицо-Индивидуальный предприниматель – представитель юридического лица (ФЛ-ИП-ЮЛ)
        optional string SignerOrganizationName = 8; // Наименование (НаимОрг)
        optional string SignerInfo = 9;             // Иные сведения, идентифицирующие физическое лицо (ИныеСвед)
        required SignerPowers SignerPowers = 10;    // Область полномочий (ОблПолн)
        required SignerStatus SignerStatus = 11;    // Статус (Статус)
        optional string SignerPowersBase = 12;      // Основание полномочий (доверия) (ОснПолн)
        optional string SignerOrgPowersBase = 13;   // Основание полномочий (доверия) организации (ОснПолнОрг)
    }

    message ExtendedSignerDetailsToPost {
        optional string JobTitle = 1;
        optional string RegistrationCertificate = 2;
        required SignerType SignerType = 3;        // Физическое лицо-Индивидуальный предприниматель – представитель юридического лица (ФЛ-ИП-ЮЛ)
        optional string SignerInfo = 4;            // Иные сведения, идентифицирующие лицо (Юл.ИныеСвед или СвИП.ИныеСвед  или ФЛ.ИныеСвед)
        required SignerPowers SignerPowers = 5;    // Область полномочий (ОблПолн)
        required SignerStatus SignerStatus = 6;    // Статус (Статус)
        optional string SignerPowersBase = 7;      // Основание полномочий (доверия) (ОснПолн)
        optional string SignerOrgPowersBase = 8;   // Основание полномочий (доверия) организации (ОснПолнОрг)
    }

    enum SignerType {
        LegalEntity = 1;      // Представитель юридического лица
        IndividualEntity = 2; // Индивидуальный предприниматель
        PhysicalPerson = 3;   // Физическое лицо
    }

    enum SignerPowers {
        InvoiceSigner = 0;                 // лицо, ответственное за подписание счетов-фактур
        PersonMadeOperation = 1;           // лицо, совершившее сделку, операцию
        MadeAndSignOperation = 2;          // лицо, совершившее сделку, операцию и ответственное за её оформление;
        PersonDocumentedOperation = 3;     // лицо, ответственное за оформление свершившегося события;
        MadeOperationAndSignedInvoice = 4; // лицо, совершившее сделку, операцию и ответственное за подписание счетов-фактур;
        MadeAndResponsibleForOperationAndSignedInvoice = 5; // лицо, совершившее сделку, операцию и ответственное за её оформление и за подписание счетов-фактур;
        ResponsibleForOperationAndSignerForInvoice = 6;     // лицо, ответственное за оформление свершившегося события и за подписание счетов-фактур
    }

    enum SignerStatus {
        SellerEmployee = 1;             // Работник организации продавца товаров (работ, услуг, имущественных прав);
        InformationCreatorEmployee = 2; // Работник организации - составителя информации продавца;
        OtherOrganizationEmployee = 3;  // Работник иной уполномоченной организации;
        AuthorizedPerson= 4;            // Уполномоченное физическое лицо (в том числе индивидуальный предприниматель)
    }

Структура данных *ExtendedSigner* содержит следующие поля:

-  *Surname* - фамилия подписанта.

-  *FirstName* - имя подписанта.

-  *Patronymic* - отчество подписанта (необязательно).

-  *JobTitle* - должность подписанта.    

-  *Inn* - ИНН юридического лица подписанта или индивидуального предпринимателя (необязательно).

-  *SoleProprietorRegistrationCertificate* - реквизиты свидетельства о регистрации индивидуального предпринимателя (необязательно).

- *SignerType* - ТИП подписанта: индивидуальный предприниматель, юридическое или физическое лицо

- *SignerInfo* - иные сведения, идентифицируеющие подписанта.

- *SignerPowers* - область полномочий подписанта. Указывается из предложенного списка.

- *SignerStatus* - статус подписанта. Указывается из предложенного списка.

- *SignerPowersBase* - основания полномочий (доверия) подписанта. Обязателен, если SignerStatus = 4, "уполномоченное физическое лицо"

- *SignerOrgPowersBase* - основания полномочий (доверия) организации. Обязателен, если SignerStatus = 3, "работник иной уполномоченной организации"