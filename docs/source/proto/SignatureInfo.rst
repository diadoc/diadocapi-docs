SignatureInfo
=============

Структура ``SignatureInfo`` хранит информацию о подписи и сертификате. 

.. code-block:: protobuf

   message SignatureInfo 
    {
        required Timestamp SigningTime = 1;
        optional Timestamp SignatureVerificationTime = 2;
        optional SignatureVerificationResult SignatureVerificationResult = 3;
        required string Thumbprint = 4;
        required string SerialNumber = 5;
        optional string Issuer = 6;
        optional string StartDate = 7;
        optional string EndDate = 8;
        optional string OrgName = 9;
        optional string OrgInn = 10;
        optional string JobTitle = 11;
        optional string FirstName = 12;
        optional string Surname = 13;
        optional string Snils = 14;
        optional string Email = 15;
        optional CertificateSubjectType CertificateSubjectType = 16;
    }

    enum CertificateSubjectType {
        UnknownCertificateSubjectType = 0;
        LegalEntity = 1;
        IndividualEntity = 2;
        PhysicalPerson = 3;
    }


- ``SigningTime`` — время формирования подписи, представленное структурой :doc:`Timestamp`.
- ``SignatureVerificationTime`` — время проверки подписи, представленное структурой :doc:`Timestamp`.
- ``SignatureVerificationResult`` — результат проверки подписи, представленный структурой :doc:`SignatureVerificationResult`.
- ``Thumbprint`` — отпечаток сертификата.
- ``SerialNumber`` — серийный номер сертификата.
- ``Issuer`` — кем выдан сертификат.
- ``StartDate`` — дата начала действия сертификата.
- ``EndDate`` — дата окончания действия сертификата.
- ``OrgName`` — наименование организации.
- ``OrgInn`` — ИНН организации.
- ``JobTitle`` — должность владельца сертификата.
- ``FirstName`` — имя и отчество (если есть) владельца сертификата.
- ``Surname`` — фамилия владельца сертификата.
- ``Snils`` — СНИЛС владельца сертификата.
- ``Email`` — электронная почта владельца сертификата.
- ``CertificateSubjectType`` — тип владельца сертификата, принимает значение из перечисления ``CertificateSubjectType``:

	- ``UnknownCertificateSubjectType`` — тип неопределен;
	- ``LegalEntity`` — юридическое лицо;
	- ``IndividualEntity`` — индивидуальный предприниматель;
	- ``PhysicalPerson`` — физическое лицо.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetSignatureInfo`

*Определение:*
	- :doc:`../entities/signature`