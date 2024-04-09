CertificateInfoV2
=================

Структура ``CertificateInfoV2`` хранит информацию о сертификате пользователя.

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

Структура ``CertificateList`` предназначена для хранения списка сертификатов, представленных структой ``CertificateInfoV2``.

- ``Thumbprint`` — отпечаток сертификата пользователя.
- ``Type`` — тип сертификата, принимает значения из перечисления ``CertificateType``:

	- ``Unknown`` — неизвестный тип сертификата, значение по умолчанию;
	- ``Token`` — железный носитель
	- ``DSS`` — сертификат myDSS и Контур.Подпись;
	- ``KonturCertificate`` — сертификат облачной неквалифицированной электронной подписи (ОНЭП).

- ``ValidFrom`` — дата начала действия сертификата, ticks.
- ``ValidTo`` — дата окончания действия сертификата, ticks.
- ``PrivateKeyValidFrom`` — дата начала действия закрытого ключа, ticks.
- ``PrivateKeyValidTo`` — дата окончания действия закрытого ключа, ticks.
- ``OrganizationName`` — наименование организации, на которую выдан сертификат.
- ``Inn`` — ИНН организации, на которую выдан сертификат.
- ``UserFirstName`` — имя пользователя.
- ``UserMiddleName`` — отчество пользователя.
- ``UserLastName`` — фамилия пользователя.
- ``UserShortName`` — краткое имя пользователя в формате «Фамилия И.О.».
- ``IsDefault`` — признак, означающий, выбран ли сертификат для работы по умолчанию в организации сотрудника. Например, от этого зависит автоматическое подписание извещений о получений в веб-интерфейсе Диадока.
- ``SubjectType`` — тип владельца сертификата, принимает значения из перечисления ``CertificateSubjectType``:

	- ``UnknownCertificateSubjectType`` — неизвестный тип владельца, значение по умолчанию;
	- ``LegalEntity`` — представитель юридического лица;
	- ``IndividualEntity`` — индивидуальный предприниматель;
	- ``PhysicalPerson`` — физическое лицо.


----

.. rubric:: Смотри также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetMyCertificates`.