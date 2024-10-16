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

	- ``JobTitle`` — должность подписанта.

	  Обязательно к заполнению в методах:

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

В структуре должно быть указано хотя бы одно значение из следующих:

	- поле ``SignerCertificate`` или ``SignerCertificateThumbprint``.
	- поле ``SignerDetails``.

Если вы указали данные сертификата, то реквизиты подписанта извлекаются из сертификата.
Если вы указали и данные сертификата, и ``SignerDetails``, то для реквизитов используются значения из ``SignerDetails``.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`ContentToPatch <PrepareDocumentsToSignRequest>`
	- в структуре :doc:`DocumentToPatch <PrepareDocumentsToSignRequest>`
	- в структуре :doc:`DraftDocumentToPatch <PrepareDocumentsToSignRequest>`
	- в структуре :doc:`InvoiceCorrectionRequestInfo`
	- в структуре :doc:`RevocationRequestInfo`
	- в структуре :doc:`SignatureRejectionInfo`
	- в устаревшей структуре :doc:`AcceptanceCertificateBuyerTitleInfo <obsolete/AcceptanceCertificateInfo>`
	- в устаревшей структуре :doc:`AcceptanceCertificateSellerTitleInfo <obsolete/AcceptanceCertificateInfo>`
	- в устаревшей структуре :doc:`obsolete/InvoiceCorrectionInfo`
	- в устаревшей структуре :doc:`obsolete/InvoiceInfo`
	- в устаревшей структуре :doc:`Torg12BuyerTitleInfo <obsolete/Torg12Info>`
	- в устаревшей структуре :doc:`Torg12SellerTitleInfo <obsolete/Torg12Info>`
	- в теле запроса устаревшего метода :doc:`GenerateReceiptXml <../http/GenerateReceiptXml>`