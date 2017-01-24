CertificateVerificationResult
=============================

.. code-block:: protobuf

   message CertificateVerificationResult
   {
       required bool IsValid = 2;
       repeated CertificateChainElement CertificateChain = 3;
       required Timestamp VerificationTime = 4;
   }

Структура представляет отчет о проверке сертификата ЭП.

-  *IsValid* - общий признак корректности сертификата (все ли проверки прошли успешно).
-  :doc:`CertificateChain <CertificateChainElement>` - информация о цепочке сертификатов, участвовавших в проверке ЭП. Первый элемент в массиве описывает конечный сертификат пользователя, а последний - сертификат корневого УЦ.
-  :doc:`VerificationTime <Timestamp>` - момент времени, в который (и на который) производилась проверка.
