ExtendedSignerToPost
====================

.. code-block:: protobuf
   :emphasize-lines: 1-6

     message ExtendedSignerToPost {
        optional string JobTitle = 1; //Должность (Должн)
        optional string RegistrationCertificate = 2; //Реквизиты свидетельства о государственной регистрации индивидуального предпринимателя (СвГосРегИП)
        required SignerType SignerType = 3 [default = LegalEntity]; // Тип подписанта (ФЛ/ИП/ЮЛ)
        optional string SignerInfo = 4;             // Иные сведения, идентифицирующие физическое лицо (ИныеСвед)
        required SignerPowers SignerPowers = 5;    // Область полномочий (ОблПолн)
        required SignerStatus SignerStatus = 6;    // Статус (Статус)
        optional string SignerPowersBase = 7;      // Основание полномочий (доверия) (ОснПолн)
        optional string SignerOrgPowersBase = 8;   // Основание полномочий (доверия) организации (ОснПолнОрг)
      }


     enum SignerType {
        LegalEntity = 1;      // Представитель юридического лица (ФЛ)
        IndividualEntity = 2; // Индивидуальный предприниматель (ИП)
        PhysicalPerson = 3;   // Физическое лицо (ЮЛ)
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

Структура данных *ExtendedSignerToPost* используется для записи данных о подписанте в базу данных и содержит следующие поля:

-  *JobTitle* - должность подписанта.    

-  *SoleProprietorRegistrationCertificate* - реквизиты свидетельства о регистрации индивидуального предпринимателя (необязательно).

- *SignerType* - ТИП подписанта: индивидуальный предприниматель, юридическое или физическое лицо

- *SignerInfo* - иные сведения, идентифицируеющие подписанта.

- *SignerPowers* - область полномочий подписанта. Указывается из предложенного списка.

- *SignerStatus* - статус подписанта. Указывается из предложенного списка.

- *SignerPowersBase* - основания полномочий (доверия) подписанта. Обязателен, если SignerStatus = 4, "уполномоченное физическое лицо"

- *SignerOrgPowersBase* - Основания полномочий (доверия) организации. Обязателен, если SignerStatus = 3, "работник иной уполномоченной организации""

