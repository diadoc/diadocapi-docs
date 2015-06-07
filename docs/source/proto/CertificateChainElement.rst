CertificateChainElement
=======================

.. code-block:: protobuf

    message CertificateChainElement
    {
        required int32 CertificateChainStatusFlags = 1;
        required bytes DerCertificate = 2;
    }

Структура содержит информацию о результатах проверки для отдельного сертификата в цепочке, выстроенной при проверке конечного сертификата пользователя.

-  *CertificateChainStatusFlags* - статус элемента цепочки сертификатов. 

	Представляет собой комбинацию битовых флагов из .NET-перечисления `System.Security.Cryptography.X509Certificates.X509ChainStatusFlags <https://msdn.microsoft.com/en-us/library/system.security.cryptography.x509certificates.x509chainstatusflags.aspx>`__.
	
-  *DerCertificate* - сам сертификат, сериализованный в массив байтов в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке.