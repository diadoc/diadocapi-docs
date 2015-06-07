Signature
=========

.. code-block:: protobuf

   message Signature
   {
       optional Entity Entity = 1;
       optional string SignerBoxId = 2;
       optional string SignerDepartmentId = 3;
       optional bool IsValid = 4;
       optional SignatureVerificationResult VerificationResult = 5;
   }

Структура представляет информацию о подписи под документом.

-  :doc:`Entity` - информация о содержимом подписи.
-  *SignerBoxId* - идентификатор ящика, от имени которого была поставлена подпись.
-  *SignerDepartmentId* - идентификатор подразделения, сотрудник которого поставил подпись.
-  *IsValid* - признак того, что подпись либо еще не прошла проверку, либо проверена и признана верной.
-  :doc:`VerificationResult <SignatureVerificationResult>` - результат проверки подписи.
