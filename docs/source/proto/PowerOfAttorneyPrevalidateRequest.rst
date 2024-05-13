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
	- ``Content`` — сертификат пользователя, представленный структурой :doc:`../proto/Content_v3`.
	
В структуре должно быть заполнено только одно из полей: ``Thumbprint`` или ``Content``.

----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/PrevalidatePowerOfAttorney`

*Инструкции:*
	- :doc:`../instructions/powerofattorney`