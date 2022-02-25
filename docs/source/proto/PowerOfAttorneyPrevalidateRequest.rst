PowerOfAttorneyPrevalidateRequest
=================================

Структура ``PowerOfAttorneyPrevalidateRequest`` хранит данные для :doc:`предварительной проверки <../http/PrevalidatePowerOfAttorney>` машиночитаемой доверенности (МЧД).

.. code-block:: protobuf

    message PowerOfAttorneyPrevalidateRequest{
        required ConfidantCertificateToPrevalidate ConfidantCertificate = 1;
    }
  
    message ConfidantCertificateToPrevalidate {
        optional string Thumbprint = 1;
        optional Content_v3 Content = 2;
    }

- ``ConfidantCertificateToPrevalidate`` — данные о сертификате, которым планируется подписывать документ с МЧД. Представлены структурой ``ConfidantCertificateToPrevalidate`` с полями:

	- ``Thumbprint`` — отпечаток сертификата.
	- ``Content`` — сертификат пользователя, сериализованный в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__.

----

.. rubric:: Использование

Структура ``PowerOfAttorneyPrevalidateRequest`` используется в теле запроса метода :doc:`../http/PrevalidatePowerOfAttorney`.