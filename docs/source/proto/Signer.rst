Signer
======

Структура ``Signer`` представляет собой информацию о подписанте документа.

.. code-block:: protobuf

    message Signer {
        optional bytes SignerCertificate = 1;
        optional SignerDetails SignerDetails = 2;
        optional string SignerCertificateThumbprint = 3;
    }

    message SignerDetails {
        required string Surname = 1;
        required string FirstName = 2;
        optional string Patronymic = 3;
        optional string JobTitle = 4;
        required string Inn = 5;
        optional string SoleProprietorRegistrationCertificate = 6;
    }

- ``SignerCertificate`` — :rfc:`X.509 <5280>` сертификат подписанта в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__ - кодировке.
- ``SignerDetails`` — реквизиты подписанта. Представлены структурой ``SignerDetails`` с полями:

	- ``Surname`` — фамилия подписанта. Должна совпадать с фамилией в сертификате, которым подписывается технологический документ.
	- ``FirstName`` — имя подписанта. Должно совпадать с именем в сертификате, которым подписывается технологический документ.
	- ``Patronymic`` — отчество подписанта. Необязательное поле. Должно совпадать с именем в сертификате, которым подписывается технологический документ.

	- ``JobTitle`` — должность подписанта. Обязательно к заполнению в методах:

		- :doc:`../http/GenerateInvoiceCorrectionRequestXml`
		- :doc:`../http/GenerateReceiptXml`
		- :doc:`../http/GenerateSignatureRejectionXml`
		- :doc:`../http/GenerateRevocationRequestXml`

		Необязательно в методах:

		- :doc:`../http/obsolete/GenerateInvoiceXml`
		- :doc:`../http/obsolete/GenerateTorg12XmlForSeller`
		- :doc:`../http/obsolete/GenerateTorg12XmlForBuyer`
		- :doc:`../http/obsolete/GenerateAcceptanceCertificateXmlForSeller`
		- :doc:`../http/obsolete/GenerateAcceptanceCertificateXmlForBuyer`

	- ``Inn`` - ИНН юридического лица подписанта или индивидуального предпринимателя.
	- ``SoleProprietorRegistrationCertificate`` — реквизиты свидетельства о регистрации индивидуального предпринимателя. Необязательное поле.

- ``SignerCertificateThumbprint`` - отпечаток сертификата подписанта.

Одно из полей ``SignerCertificate`` или ``SignerDetails`` должно быть заполнено. Если заполнено поле ``SignerCertificate``, реквизиты подписанта извлекаются из сертификата. Если заполнены оба поля — используется поле ``SignerDetails``.

