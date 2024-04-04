RegistrationRequest
===================

Структура ``RegistrationRequest`` представляет собой запрос на регистрацию в организации по сертификату.

.. code-block:: protobuf

    message RegistrationRequest {
        optional bytes CertificateContent = 1;
        optional string Thumbprint = 2;
    }

- ``CertificateContent`` — :rfc:`X.509 <5280>` сертификат пользователя, сериализованный в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__. Не может быть заполнено одновременно с ``Thumbprint``.
- ``Thumbprint`` — отпечаток сертификата пользователя.

Сертификат должен быть квалифицированным, действующим и настроенным для работы в Диадоке пользователем, от имени которого выполняется запрос.

----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/Register`