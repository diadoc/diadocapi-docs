ExtendedSignerDetails
=====================

Структура ``ExtendedSignerDetails`` содержит информацию о реквизитах подписанта.

.. code-block:: protobuf

    message ExtendedSignerDetails {
        required string Surname = 1;
        required string FirstName = 2;
        optional string Patronymic = 3;
        optional string JobTitle = 4;
        optional string Inn = 5;
        optional string RegistrationCertificate = 6;
        required SignerType SignerType = 7;
        optional string SignerOrganizationName = 8;
        optional string SignerInfo = 9;
        required SignerPowers SignerPowers = 10;
        required SignerStatus SignerStatus = 11;
        optional string SignerPowersBase = 12;
        optional string SignerOrgPowersBase = 13;
    }

- ``Surname`` — фамилия подписанта.
- ``FirstName`` — имя подписанта.
- ``Patronymic`` — отчество подписанта. Необязательное поле.
- ``JobTitle`` — должность подписанта.
- ``Inn`` — ИНН юридического лица подписанта или индивидуального предпринимателя. Необязательное поле.
- ``RegistrationCertificate`` — реквизиты свидетельства о регистрации индивидуального предпринимателя. Необязательное поле.
- ``SignerType`` — тип подписанта, принимает значения из перечисления :doc:`SignerType`.
- ``SignerInfo`` — иные сведения, идентифицируеющие подписанта.
- ``SignerPowers`` — область полномочий подписанта, принимает значения из перечисления :doc:`SignerPowers`.
- ``SignerStatus`` — статус подписанта, принимает значения из перечисления :doc:`SignerStatus`.
- ``SignerPowersBase`` — основания полномочий (доверия) подписанта. Обязателен, если ``SignerStatus = 4``.
- ``SignerOrgPowersBase`` — основания полномочий (доверия) организации. Обязателен, если ``SignerStatus = 3``.
- ``SignerOrganizationName`` — наименование организации. Обязателен при вызове метода :doc:`../../http/PrepareDocumentsToSign`, если одновременно выполняются следующие условия:

	- ``SignerType = LegalEntity``,
	- поле ``TypeNamedId`` структуры :doc:`PrepareDocumentsToSignRequest` имеет значение ``XmlAcceptanceCertificate`` или ``XmlTorg12``,
	- поле ``Version`` структуры :doc:`PrepareDocumentsToSignRequest` имеет одно из следующих значений:

		- ``tovtorg_05_01_02``,
		- ``tovtorg_05_01_03``,
		- ``tovtorg_05_01_04``,
		- ``tovtorg_05_02_01``,
		- ``rezru_05_01_01``,
		- ``rezru_05_01_02``,
		- ``rezru_05_02_01``.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`utd/ExtendedSigner`,
	- в теле ответа метода :doc:`../../http/utd/ExtendedSignerDetailsV2`.
