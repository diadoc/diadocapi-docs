RegistrationConfirmRequest
==========================

.. code-block:: protobuf

    message RegistrationConfirmRequest {
        optional bytes CertificateContent = 1;
        optional string Thumbprint = 2;
        required bytes DataToSign  = 3;
        required bytes Signature = 4;
    }

Содержит данные для подтверждения владения закрытым ключом сертификата. Принимается методом :doc:`../http/RegisterConfirm`.

 - *CertificateContent* - :rfc:`X.509 <5280>` сертификат пользователя, сериализованный в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__
 - *Thumbprint* - отпечаток сертификата пользователя
 - *DataToSign* — контент, возвращенный методом :doc:`../http/Register`
 - *Signature* — подпись под контентом *DataToSign* в формате :rfc:`CMS SignedData <5652#section-5>` в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке

Должно быть заполнено ровно одно из полей *CertificateContent* и *Thumbprint*.
