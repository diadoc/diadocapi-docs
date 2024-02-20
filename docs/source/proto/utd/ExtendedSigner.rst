ExtendedSigner
==============

Структура ``ExtendedSigner`` представляет собой информацию о подписанте документа.

.. code-block:: protobuf

    message ExtendedSigner {
        optional string BoxId = 1;
        optional bytes SignerCertificate = 2;
        optional string SignerCertificateThumbprint = 3;
        optional ExtendedSignerDetails SignerDetails = 4;
        optional PowerOfAttorneyToPost PowerOfAttorney = 5;
    }


- ``BoxId`` — идентификатор ящика организации.
- ``SignerCertificate`` — :rfc:`X.509 <5280>` сертификат подписанта в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__ - кодировке.
- ``SignerCertificateThumbprint`` — отпечаток сертификата подписанта.
- ``SignerDetails`` — реквизиты подписанта, представленные структурой :doc:`ExtendedSignerDetails`.
- ``PowerOfAttorney`` — данные машиночитаемой доверенности, представленные структурой :doc:`../PowerOfAttorneyToPost`.
