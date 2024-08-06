CertificateList
===============

Структура ``CertificateList`` представляет собой список :doc:`сертификатов <../entities/certificate>`.

.. code-block:: protobuf

    message CertificateList {
        repeated CertificateInfoV2 Certificates = 1;
    }

    message CertificateInfoV2 {
        required string Thumbprint = 1;
        required CertificateType Type = 2;
        optional sfixed64 ValidFrom = 3;
        optional sfixed64 ValidTo = 4;
        optional sfixed64 PrivateKeyValidFrom = 5;
        optional sfixed64 PrivateKeyValidTo = 6;
        optional string OrganizationName = 7;
        optional string Inn = 8;
        optional string UserFirstName = 9;
        optional string UserMiddleName = 10;
        optional string UserLastName = 11;
        optional string UserShortName = 12;
        optional bool IsDefault = 13;
        optional CertificateSubjectType SubjectType = 14;
        repeated CertificateUsage Usages = 15;
        optional DssCertificateType DssType = 16;
    }

    enum CertificateType {
        Unknown = 0;
        Token = 1;
        DSS = 2;
        KonturCertificate = 3;
    }

    enum CertificateSubjectType {
        UnknownCertificateSubjectType = 0;
        LegalEntity = 1;
        IndividualEntity = 2;
        PhysicalPerson = 3;
    }

    enum CertificateUsage {
        UnknownUsage = 0;
        KonturCertificateUsage = 1;
        TokenUsage = 2;
        DssUsage = 3;
    }

    enum DssCertificateType {
        UnknownDssType = 0;
        MyDss = 1;
        KSignServer = 2;
        KSignRutoken = 3;
        KSignMobile = 4;
    }

- ``Certificates`` — список сертификатов. Каждый элемент списка представлен структурой ``CertificateInfoV2`` с полями: 

	- ``Thumbprint`` — отпечаток сертификата пользователя.
	- ``Type`` — тип сертификата, принимает значения из перечисления ``CertificateType``:

		- ``Unknown`` — неизвестный тип сертификата;
		- ``Token`` — железный носитель;
		- ``DSS`` — сертификат myDSS и Контур.Подпись;
		- ``KonturCertificate`` — сертификат облачной неквалифицированной электронной подписи (ОНЭП).

	- ``ValidFrom`` — дата начала действия сертификата, представляет собой целое число тиков, прошедших с момента времени 00:00:00 01.01.0001.
	- ``ValidTo`` — дата окончания действия сертификата, представляет собой целое число тиков, прошедших с момента времени 00:00:00 01.01.0001.
	- ``PrivateKeyValidFrom`` — дата начала действия закрытого ключа, представляет собой целое число тиков, прошедших с момента времени 00:00:00 01.01.0001.
	- ``PrivateKeyValidTo`` — дата окончания действия закрытого ключа, представляет собой целое число тиков, прошедших с момента времени 00:00:00 01.01.0001.
	- ``OrganizationName`` — наименование организации, на которую выдан сертификат.
	- ``Inn`` — ИНН организации, на которую выдан сертификат.
	- ``UserFirstName`` — имя пользователя.
	- ``UserMiddleName`` — отчество пользователя.
	- ``UserLastName`` — фамилия пользователя.
	- ``UserShortName`` — краткое имя пользователя в формате «Фамилия И.О.».
	- ``IsDefault`` — флаг, указывающий, выбран ли сертификат для работы по умолчанию в организации сотрудника. Например, от этого зависит автоматическое подписание извещений о получений в веб-интерфейсе Диадока.
	- ``SubjectType`` — тип владельца сертификата, принимает значения из перечисления ``CertificateSubjectType``:

		- ``UnknownCertificateSubjectType`` — неизвестный тип владельца;
		- ``LegalEntity`` — представитель юридического лица;
		- ``IndividualEntity`` — индивидуальный предприниматель;
		- ``PhysicalPerson`` — физическое лицо.

	- ``Usages`` — список типов сертификата. Может быть пустым. Каждый элемент списка принимает значение из перечисления ``CertificateUsage``:

		- ``UnknownUsage`` — неизвестный тип сертификата;
		- ``KonturCertificateUsage`` — Контур.Сертификат;
		- ``TokenUsage`` — сертификат на железном носителе;
		- ``DssUsage`` — DSS-сертификат.

	- ``DssType`` — тип DSS сертификата. Если используется не DSS-сертификат, значение будет пустым. Принимает значение из перечисления ``DssCertificateType``:

		- ``UnknownDssType`` — неизвестный тип сертификата;
		- ``MyDss`` — MyDss-сертификат;
		- ``KSignServer`` — КПодпись.Сервер;
		- ``KSignRutoken`` — КПодпись.Рутокен;
		- ``KSignMobile`` — КПодпись.Мобильный.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetMyCertificates`