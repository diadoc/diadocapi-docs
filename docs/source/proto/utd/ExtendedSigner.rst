ExtendedSigner
==============

.. code-block:: protobuf

    message ExtendedSigner {
        optional string BoxId = 1;
        optional bytes SignerCertificate = 2;
        optional string SignerCertificateThumbprint = 3;
        optional ExtendedSignerDetails SignerDetails = 4;
        optional PowerOfAttorneyToPost PowerOfAttorney = 5;
    }

    message ExtendedSignerDetails {
        required string Surname = 1;
        required string FirstName = 2;
        optional string Patronymic = 3;
        optional string JobTitle = 4;
        optional string Inn = 5;
        optional string RegistrationCertificate = 6;

        required SignerType SignerType = 7 [default = LegalEntity]; // Физическое лицо-Индивидуальный предприниматель – представитель юридического лица (ФЛ-ИП-ЮЛ)
        optional string SignerOrganizationName = 8;                 // Наименование (НаимОрг)
        optional string SignerInfo = 9;                             // Иные сведения, идентифицирующие физическое лицо (ИныеСвед)
        required SignerPowers SignerPowers = 10;                    // Область полномочий (ОблПолн)
        required SignerStatus SignerStatus = 11;                    // Статус (Статус)
        optional string SignerPowersBase = 12;                      // Основание полномочий (доверия) (ОснПолн)
        optional string SignerOrgPowersBase = 13;                   // Основание полномочий (доверия) организации (ОснПолнОрг)
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

- ``PowerOfAttorney`` — данные машиночитаемой доверенности, представленные структурой :doc:`../PowerOfAttorneyToPost`.
	
Структура данных ``ExtendedSigner`` содержит следующие поля:

- ``Surname`` — фамилия подписанта.

- ``FirstName`` — имя подписанта.

- ``Patronymic`` — отчество подписанта (необязательно).

- ``JobTitle`` — должность подписанта.

- ``Inn`` — ИНН юридического лица подписанта или индивидуального предпринимателя (необязательно).

- ``RegistrationCertificate`` — реквизиты свидетельства о регистрации индивидуального предпринимателя (необязательно).

- ``SignerType`` — тип подписанта, принимает значения из перечисления :doc:`SignerType`.

- ``SignerInfo`` — иные сведения, идентифицируеющие подписанта.

- ``SignerPowers`` — область полномочий подписанта, принимает значения из перечисления :doc:`SignerPowers`.

- ``SignerStatus`` — статус подписанта, принимает значения из перечисления :doc:`SignerStatus`.

- ``SignerPowersBase`` — основания полномочий (доверия) подписанта. Обязателен, если SignerStatus = 4, "уполномоченное физическое лицо"

- ``SignerOrgPowersBase`` — основания полномочий (доверия) организации. Обязателен, если SignerStatus = 3, "работник иной уполномоченной организации"

- ``SignerOrganizationName`` — наименование организации. Элемент является обязательным, если выполняются следующие условия:

    - ``SignerType = LegalEntity``

    - ``AttachmentVersion = tovtorg_05_01_02`` или ``rezru_05_01_01``

    - вызван метод :doc:`../../obsolete/http/GenerateTorg12XmlForSeller`, :doc:`../../obsolete/http/GenerateTorg12XmlForBuyer`, :doc:`../../obsolete/http/GenerateAcceptanceCertificateXmlForSeller` или :doc:`../../obsolete/http/GenerateAcceptanceCertificateXmlForBuyer`
