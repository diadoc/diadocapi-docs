CertificateVerificationResult
=============================

Структура ``CertificateVerificationResult`` хранит информацию о проверке :doc:`сертификата <../entities/certificate>`.

.. code-block:: protobuf

   message CertificateVerificationResult
   {
       required bool IsValid = 2;
       repeated CertificateChainElement CertificateChain = 3;
       required Timestamp VerificationTime = 4;
   }

- ``IsValid`` — флаг, указывающий, все ли проверки сертификата прошли успешно.
- ``CertificateChain`` — информация о цепочке сертификатов, участвовавших в проверке :doc:`электронной подписи <../entities/signature>`. Представлена структурой :doc:`CertificateChainElement`. Первый элемент в массиве описывает конечный сертификат пользователя, а последний — сертификат корневого УЦ.
- ``VerificationTime`` — время проверки, представленное структурой :doc:`Timestamp`.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`SignatureVerificationResult`