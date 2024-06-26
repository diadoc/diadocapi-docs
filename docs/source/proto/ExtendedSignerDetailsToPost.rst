ExtendedSignerDetailsToPost
===========================

Структура ``ExtendedSignerDetailsToPost`` хранит информацию о подписанте.

.. code-block:: protobuf

     message ExtendedSignerDetailsToPost {
         optional string JobTitle = 1;
         optional string RegistrationCertificate = 2;
         optional SignerType SignerType = 3 [default = SignerTypeUnspecified];
         optional string SignerInfo = 4;
         optional SignerPowers SignerPowers = 5 [default = SignerPowersUnspecified];
         optional SignerStatus SignerStatus = 6 [default = SignerStatusUnspecified];
         optional string SignerPowersBase = 7;
         optional string SignerOrgPowersBase = 8;
      }

- ``JobTitle`` — должность подписанта.
- ``RegistrationCertificate`` — реквизиты свидетельства о регистрации индивидуального предпринимателя.
- ``SignerType`` — тип подписанта, принимает значения из перечисления :doc:`SignerType`. По умолчанию имеет значение ``SignerTypeUnspecified``.
- ``SignerInfo`` — иные сведения, идентифицирующие подписанта.
- ``SignerPowers`` — область полномочий подписанта, принимает значения из перечисления :doc:`SignerPowers`.
- ``SignerStatus`` — статус подписанта, принимает значения из перечисления :doc:`SignerStatus`.
- ``SignerPowersBase`` — основания полномочий подписанта. Поле обязательное в случае, если ``SignerStatus = 4``.
- ``SignerOrgPowersBase`` — основания полномочий организации. Поле обязательное в случае, если ``SignerStatus = 3``.

----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../../http/ExtendedSignerDetailsV2`