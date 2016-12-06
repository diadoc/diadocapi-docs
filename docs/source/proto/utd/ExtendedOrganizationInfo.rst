ExtendedOrganizationInfo
========================

.. code-block:: protobuf
    :emphasize-lines: 1-22

    message ExtendedOrganizationInfo {
        optional string BoxId = 1;
        optional string OrgName = 2;
        optional string Inn = 3; 
        optional string Kpp = 4;
        optional Address Address = 5;
        optional string FnsParticipantId = 6;
        required OrgType OrgType = 7;
        optional string Okopf = 8;
        optional string Okpo = 9;
        optional string Okdp = 10;
        optional string Phone = 11;
        optional string Email = 12;
        optional string CorrespondentAccount = 13;
        optional string BankAccountNumber = 14;
        optional string BankName = 15;
        optional string BankId = 16;
        optional string Department = 17;
        optional string OrganizationAdditionalInfo = 18;
        optional string OrganizationOrPersonInfo = 19;
        optional string IndividualEntityRegistrationCertificate = 20;
    }
  
    enum OrgType {
        LegalEntity = 1;      // Сведения о юридическом лице, состоящем на учете в налоговых органах
        IndividualEntity = 2; // Сведения об индивидуальном предпринимателе//
        ForeignEntity = 3;    // Сведения об иностранном лице, не состоящем на учете в налоговых органах //
    }
        

Структура данных *ExtendedOrganizationInfo* служит для представления реквизитов организаций-контрагентов при формирования счетов-фактур (см. :doc:`../InvoiceInfo`), товарных накладных (см. :doc:`Torg12SellerTitleInfo <../Torg12Info>`), актов о выполнении работ / оказании услуг (см. :doc:`AcceptanceCertificateSellerTitleInfo <../AcceptanceCertificateInfo>`) и универасальных передаточных документов в "новом" XML-формате.

В зависимости от контекста использования структуры *ExtendedOrganizationInfo* требования к обязательности заполнения ее полей могут меняться. Однако в любом случае всегда требуется указывать название организации (*ExtendedOrganizationInfo.Name*) и ее адрес (:doc:`ExtendedOrganizationInfo.Address <../Address>`). 

На текущий момент структура используется для заполнения сведений об организацях в документах в формате УПД.

Структура данных *ExtendedOrganizationInfo* содержит в себе следующие поля:

-  *BoxId* - при заполнении BoxID в протобуфер подставляются значени *OrgName, Inn, Kpp, Address, FnsParticipantId*. 

-  *OrgName* - наименование организации (НаимОрг)

-  *Inn* - ИНН организации (ИННФЛ/ИНН)

-  *Kpp* - КПП организации (КПП)

-  *Address* - адрес, передаётся в структуре :doc: `../Address` (Адрес)

-  *FnsParticipantId* - ФНС идентификатор участника электронного документоооборота

-  *OrgType* - тип юридического лица. (СвИП/СвЮЛУч/СвИнНеУч) Возможные варианты:

  -  *LegalEntity* - юридическое лицо (СвЮЛУч)

  -  *IndividualEntity* - индивидуальный предприниматель (СвИП)

  -  *ForeignEntity* - зарубежное юридическое лицо (СвИнНеУч)

-  *Okopf* - код организационно-правововой формы по ОКОПФ

-  *Okpo* - код в общероссийском классификаторе органищаций и предприятий, ОКПО

-  *Okdp* - код основного вида деятельности по ОКДП

-  *Phone* - номер контактного телефона и/или номер факса. (Тлф) В отличие от протобуфере :doc:`../OrganizationInfo` для телефона и факса используется одно поле

-  *Email* - контактный Email (ЭлПочта)

-  *CorrespondentAccount* - кор. счёт (КорСчет)

-  *BankAccountNumber* - номер банковского счета организации (НомерСчета)

-  *BankName* - наименование банка (НаимБанк)

-  *BankId* - банковский идентификационный код (БИК)

-  *Department* - структурное подразделение организации, указывается если в контексте использования протобуфера помогает для идентификации лица (СтруктПодр)

-  *OrganizationOrPersonInfo* - иные сведения, идентифицирующие лицо (ИнфДляУчаст)

-  *IndividualEntityRegistrationCertificate* - реквизиты свидетельства о государственной регистрации ИП (СвГосРегИп)