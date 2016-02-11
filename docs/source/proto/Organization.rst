Organization
============

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
    }

    message Box {
        required string BoxId = 1;
        required string Title = 2;
        optional Organization Organization = 3;
        optional OrganizationInvoiceFormatVersion InvoiceFormatVersion = 4 [default = v5_02];
    }

    enum OrganizationInvoiceFormatVersion {
        v5_01 = 1;
        v5_02 = 2;
    }

Структура данных *Organization* содержит информацию об одной организации в Диадоке: 

-  идентификатор, ИНН-КПП, ОГРН, полное и краткое наименование, список ее ящиков;

-  поле *FnsParticipantId* содержит зарегистрированный в ФНС идентификатор участника документооборота СФ, предусмотренный порядком обмена ЭСФ, который был назначен данной организации;

-  поле *FnsRegistrationDate* содержит дату подачи заявления в ФНС на регистрацию данной организации в качестве участника документооборота ЭСФ;

-  поле *IfnsCode* может содержать код налоговой инспекции - место подачи декларации по НДС; 

-  поле *IsTest* содержит признак того, что организация работает в тестовом режиме; 

-  поле *IsPilot* содержит признак того, что организация работает в пилотном режиме; 

-  поле *IsActive* содержит признак активности организации в Диадоке; 

-  поле *IsBranch* содержит признак того, что организация является филиалом; 

-  поле *IsRoaming* содержит признак того, что организация работает через роуминг, то есть подключена к другому оператору ЭДО. Кроме того, если у организации в Диадоке заполнен юридический адрес, то он включается в *Organization* в виде структуры :doc:`Address <Address>`;

-  поле *IsEmployee* содержит признак того, что пользователь является сотрудником организации. Используется только в методе :doc:`../http/GetMyOrganizations`;

-  поле *Departments* содержит список видимых пользователю подразделений (см. :doc:`Department`) в организации (кроме головного).

Структура данных *Box* содержит информацию об одном ящике в Диадоке: его идентификатор, понятное имя и информацию об организации-владельце ящика.

Поле *Box.Organization* заполняется в том и только в том случае, когда структура Box формируется методом :doc:`../http/GetBox`. В остальных случаях *Box* выдается в составе структуры *Organization* и там поле *Box.Organization* представляло бы циклическую ссылку.

Поле *Box.InvoiceFormatVersion* представляет версию СФ, которая используется по умолчанию в данном ящике.
