Organization
============

Структура ``Organization`` предназначена для хранения информации об одной организации в Диадоке.

.. code-block:: protobuf

    message OrganizationList {
        repeated Organization Organizations = 1;
    }

    message Organization {
        required string OrgId = 1;
        required string Inn = 2;
        optional string Kpp = 3;
        required string FullName = 4;
        optional string ShortName = 5;
        repeated Box Boxes = 7;
        optional string Ogrn = 8;
        optional string FnsParticipantId = 9;
        optional Address Address = 10;
        optional string FnsRegistrationDate = 11;
        repeated Department Departments = 12;
        optional string IfnsCode = 13;
        optional bool IsPilot = 14;
        optional bool IsActive = 15;
        optional bool IsTest = 16;
        optional bool IsBranch = 17;
        optional bool IsRoaming = 18;
        optional bool IsEmployee = 19;
        optional int32 InvitationCount = 20;
        optional int32 SearchCount = 21;
        required Sociability Sociability = 22;
        optional string LiquidationDate = 23;
        optional string CertificateOfRegistryInfo = 24;
        optional bool IsForeign = 25;
        optional bool HasCertificateToSign = 26;
    }

    enum Sociability {
        AllOrganizations = 0;
        CounteragentsOnly = 1;
    }

Структура ``OrganizationList`` предназначена для хранения списка организаций, представленных структой ``Organization``.

- ``OrgId`` — идентификатор организации.
- ``Inn`` — ИНН организации.
- ``Kpp`` — КПП организации.
- ``FullName`` — полное наименование организации.
- ``ShortName`` — краткое наименование организации.
- ``Boxes`` — список ящиков организации, представленных структурой :doc:`Box`.
- ``Ogrn`` — ОГРН организации.
- ``FnsParticipantId`` — зарегистрированный в ФНС идентификатор участника документооборота счетов-фактур, предусмотренный порядком обмена электронными счетами-фактурами.
- ``Address`` — адрес организации, представленный структурой :doc:`Address`.
- ``FnsRegistrationDate`` — поле устарело и не используется.
- ``Departments`` — список всех подразделений организации кроме головного, представленных структурой :doc:`Department`.
- ``IfnsCode`` — код налоговой инспекции — место подачи декларации по НДС.
- ``IsPilot`` — признак того, что организация работает в пилотном режиме.
- ``IsActive`` — признак того, что организация в Диадоке подписала или отправила хотя бы один документ или совершила действия с :doc:`приглашением контрагентов <../instructions/counteragents>`.
- ``IsTest`` — признак того, что организация работает в тестовом режиме.
- ``IsBranch`` — признак того, что организация является филиалом.
- ``IsRoaming`` — признак того, что организация работает через роуминг, то есть подключена к другому оператору ЭДО.
- ``IsEmployee`` — признак того, что текущий пользователь является сотрудником организации. Заполняется только в результате вызова метода :doc:`../http/GetMyOrganizations`.
- ``InvitationCount`` — количество запросов на приглашение к сотрудничеству, отправленных в данную организации. Заполняется только в результате вызова метода :doc:`../http/GetOrganizationsByInnKpp`.
- ``SearchCount`` — количество запросов на поиск данной организации в Диадоке.
- ``Sociability`` — свойство, регулирующее прием документов от контрагентов. Принимает значение из перечисления ``Sociability``:
	
	- ``AllOrganizations`` — организация принимает документы от всех контрагентов, кроме заблокированных, даже если приглашение не было принято;
	- ``CounteragentsOnly`` — организация принимает документы только от своих контрагентов. Отправка документов другими организациями невозможна.
	
- ``LiquidationDate`` — если организация ликвидирована, то поле содержит дату ликвидации организации по данным из ЕГРЮЛ и ЕГРИП.
- ``CertificateOfRegistryInfo`` — информация о свидетельстве о государственной регистрации.
- ``IsForeign`` — признак того, что организация являестя иностранной.
- ``HasCertificateToSign`` — признак наличия у организации сертификата для подписания документов.