OrganizationInfo
================

.. code-block:: protobuf

    message DocflowParticipant {
        optional string BoxId = 1;                             // идентификатор ящика в Диадоке
        optional string Inn = 2;                               // ИНН организации-участника обмена
        optional string Kpp = 3;                               // КПП организации-участника обмена
    }

    message DiadocOrganizationInfo {
        optional string BoxId = 1;                             // идентификатор ящика в Диадоке
        optional OrganizationInfo OrgInfo = 2;                 // реквизиты организации
    }

    message OrganizationInfo {
        required string Name = 1;                              // название
        optional string Inn = 2;                               // ИНН
        optional string Kpp = 3;                               // КПП
        required Address Address = 4;                          // адрес
        optional bool IsSoleProprietor = 5 [default = false];  // организация - это ИП
        optional string Okopf = 6;                             // код организационно-правовой формы по ОКОПФ
        optional string Okpo = 7;                              // код в общероссийском классификаторе предприятий и организаций
        optional string Okdp = 8;                              // код основного вида деятельности по ОКДП
        optional string Phone = 9;                             // телефон
        optional string Fax = 10;                              // факс
        optional string BankAccountNumber = 11;                // номер банковского счета
        optional string BankName = 12;                         // название банка
        optional string BankId = 13;                           // БИК
        optional string Department = 14;                       // структурное подразделение
        optional string FnsParticipantId = 15;                 // идентификатор участника ЭДО
    }
        

Структура данных *OrganizationInfo* служит для представления реквизитов организаций-контрагентов при формировании счетов-фактур (см. :doc:`InvoiceInfo`), товарных накладных (см. :doc:`Torg12SellerTitleInfo <Torg12Info>`) и актов о выполнении работ / оказании услуг (см. :doc:`AcceptanceCertificateSellerTitleInfo <AcceptanceCertificateInfo>`) в XML-формате.

В зависимости от контекста использования структуры *OrganizationInfo* требования к обязательности заполнения ее полей могут меняться. Однако в любом случае всегда требуется указывать название организации (*OrganizationInfo.Name*) и ее адрес (:doc:`OrganizationInfo.Address <Address>`). 

Стоит отметить, что при формировании XML счетов-фактур (при заполнении структуры *InvoiceInfo*) используются только поля *Name, Inn, Kpp, Address, IsSoleProprietor, FnsParticipantId*.

Структура данных *DiadocOrganizationInfo* также служит для представления реквизитов организаций. Она используется в тех случаях, когда организация заведомо должна быть зарегистрирована в справочнике организация Диадока (например, организация-продавец или организация-покупатель при формировании XML счета-фактуры). 

В этом случае реквизиты организации (*DiadocOrganizationInfo.OrgInfo*) можно явно не заполнять, и тогда будут использоваться данные из БД учетных записей| Диадока, ассоциированные с соответствующим ящиком (DiadocOrganizationInfo.BoxId). В структуре *DiadocOrganizationInfo* должно быть заполнено хотя бы одно из полей *BoxId*, или *OrgInfo*. Если поле *OrgInfo* заполнено, то будут использоваться данные из него; обращений к справочнику организаций Диадока не будет.

Структура данных *DocflowParticipant* содержит данные, необходимые для идентификации участника электронного документооборота. Вне зависимости от контекста использования, одно из полей *DocflowParticipant.BoxId* или *DocflowParticipant.Inn* должно быть заполнено. Для определения идентификатора участника системе требуется его ИНН-КПП, который может быть определен на основе значения *DocflowParticipant.BoxId*, если поле *DocflowParticipant.Inn* не заполнено.
