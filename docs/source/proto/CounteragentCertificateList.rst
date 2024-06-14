CounteragentCertificateList
===========================

Структура ``CounteragentCertificateList`` представляет собой список сертификатов контрагента.

.. code-block:: protobuf

    message CounteragentCertificateList {
        repeated Certificate Certificates = 1;
    }

    message Certificate {
        required bytes RawCertificateData = 1;
    }

- ``Certificates`` — список сертификатов контрагента. Каждый элемент списка представлен структурой ``Certificate`` с полями:

	- ``RawCertificateData`` — сертификат, сериализованный в массив байтов в DER-кодировке.

----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetCounteragentCertificates`

*Определение:*
	- :doc:`../entities/counteragent`
	- :doc:`../entities/certificate`

*Руководства:*

	- :doc:`../instructions/counteragents`