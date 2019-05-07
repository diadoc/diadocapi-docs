RegistrationRequest
===================

.. code-block:: protobuf

    message RegistrationRequest {
        optional bytes CertificateContent = 1;
        optional string Thumbprint = 2;
    }

Содержит запрос на регистрацию в организации по сертификату. Принимается методом :doc:`../http/Register`.

 - *CertificateContent* - :rfc:`X.509 <5280>` сертификат пользователя, сериализованный в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__
 - *Thumbprint* - отпечаток сертификата пользователя

Должно быть заполнено ровно одно из полей *CertificateContent* и *Thumbprint*.

Указанный сертификат должен быть действующим сертификатом квалифицированной электронной подписи.

Сертификат должен быть настроен для использования пользователем, от имени которого выполняется запрос, в продуктах СКБ Контур.