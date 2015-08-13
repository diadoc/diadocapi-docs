SignatureVerificationResult
===========================

.. code-block:: protobuf

   message SignatureVerificationResult
   {
       required bool IsValid = 1;
       optional CertificateVerificationResult CertificateStatus = 2;
       optional Timestamp SignatureTimestamp = 3;
   }

Структура представляет протокол проверки ЭЦП, формируемый в процессе доставки документа.

-  *IsValid* - итоговый статус проверки подписи (все ли проверки прошли успешно).

-  :doc:`CertificateStatus <CertificateVerificationResult>` - результат проверки сертификата подписанта.

-  :doc:`SignatureTimestamp <Timestamp>` - метка времени из штампа времени, который формируется Диадоком для корректных подписей в момент их проверки.
