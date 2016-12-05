ExtendedSigner
==============

.. code-block:: protobuf

 message ExtendedSigner {
    required string Surname = 1;  //Фамилия
    required string FirstName = 2; //Имя
    optional string Patronymic = 3; //Отчество
    optional string JobTitle = 4; //Должность (Должн)
    optional string Inn = 5; //ИНН подписанта (ИННФЛ/ИННЮЛ)
    optional string RegistrationCertificate = 6; //Реквизиты свидетельства о государственной регистрации индивидуального предпринимателя (СвГосРегИП)
    required SignerType SignerType = 7 [default = LegalEntity]; // Тип подписанта (ФЛ/ИП/ЮЛ)
    optional string SignerOrganizationName = 8; // Наименование (НаимОрг)
    optional string SignerInfo = 9;             // Иные сведения, идентифицирующие физическое лицо (ИныеСвед)
    required SignerPowers SignerPowers = 10;    // Область полномочий (ОблПолн)
    required SignerStatus SignerStatus = 11;    // Статус (Статус)
    optional string SignerPowersBase = 12;      // Основание полномочий (доверия) (ОснПолн)
    optional string SignerOrgPowersBase = 13;   // Основание полномочий (доверия) организации (ОснПолнОрг)
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


Структура данных ExtendedSigner содержит следующие поля:

-  Surname - фамилия подписанта.

-  FirstName - имя подписанта.

-  Patronymic - отчество подписанта (необязательно).

-  JobTitle - должность подписанта.    

-  Inn - ИНН юридического лица подписанта или индивидуального предпринимателя (необязательно).

-  SoleProprietorRegistrationCertificate - реквизиты свидетельства о регистрации индивидуального предпринимателя (необязательно).

- SignerType - ТИП подписанта: индивидуальный предприниматель, юридическое или физическое лицо

- SignerInfo - иные сведения, идентифицируеющие подписанта.

- SignerPowers - область полномочий подписанта. Указывается из предложенного списка.

- SignerStatus - статус подписанта. Указывается из предложенного списка.

- SignerPowersBase

- SignerOrgPowersBase - Основания полномочий (доверия) организации. Обязателен, если SignerStatus = 3, "работник иной уполномоченной организации""

