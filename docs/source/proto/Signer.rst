Signer
======

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
        optional string Inn = 5;
        optional string SoleProprietorRegistrationCertificate = 6;
    }
        

Структура данных Signer представляет информацию о подписанте документа. Используется в рамках документооборота счетов-фактур (СФ/ИСФ/КСФ/ИКСФ, извещение о получении, уведомление об уточнении) и некоторых других документов.

-  SignerCertificate - :rfc:`X.509 <5280>` сертификат подписанта в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__ - кодировке.

-  SignerDetails - реквизиты подписанта в виде структуры данных SignerDetails.

-  SignerCertificateThumbprint - отпечаток сертификата подписанта.

Одно из полей SignerCertificate или SignerDetails должно быть обязательно заполнено. Если заполнено поле SignerCertificate, то реквизиты подписанта извлекаются из сертификата. Если заполнены оба поля SignerCertificate и SignerDetails, то используется поле SignerDetails.

Структура данных SignerDetails содержит следующие поля:

-  Surname - фамилия подписанта.

-  FirstName - имя подписанта.

-  Patronymic - отчество подписанта (необязательно).

-  JobTitle - должность подписанта. Обязательно к заполнению при использовании в методах:

   -  :doc:`../http/GenerateInvoiceCorrectionRequestXml`

   -  :doc:`../http/GenerateInvoiceDocumentReceiptXml`

   -  :doc:`../http/GenerateSignatureRejectionXml`

   -  :doc:`../http/GenerateRevocationRequestXml`

   -  :doc:`../http/GenerateInvoiceDocumentReceiptXml`

   Не обязательно в методах:

   -  :doc:`../http/GenerateInvoiceXml`

   -  :doc:`../http/GenerateTorg12XmlForSeller`

   -  :doc:`../http/GenerateTorg12XmlForBuyer`

   -  :doc:`../http/GenerateAcceptanceCertificateXmlForSeller`

   -  :doc:`../http/GenerateAcceptanceCertificateXmlForBuyer`
   
   

-  Inn - ИНН юридического лица подписанта или индивидуального предпринимателя (необязательно).

-  SoleProprietorRegistrationCertificate - реквизиты свидетельства о регистрации индивидуального предпринимателя (необязательно).
