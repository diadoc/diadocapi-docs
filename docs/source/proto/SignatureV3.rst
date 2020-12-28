SignatureV3
===========

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message SignatureV3
    {
        required Entity Cms = 1;
        optional Entity CadesT = 2;
        required string SignerBoxId = 3;
        required string SignerDepartmentId = 4;
        required bool IsValid = 5;
        optional SignatureVerificationResult VerificationResult = 6;
        optional Timestamp DeliveredAt = 7;
    }

Структура представляет информацию о подписи под документом.

- :doc:`Cms <Entity>` - информация о содержимом оригинальной подписи
- :doc:`CadesT <Entity>` - информация о содержимом подписи в формате CADES-T
- *SignerBoxId* - идентификатор ящика, от имени которого была поставлена подпись
- *SignerDepartmentId* - идентификатор подразделения, сотрудник которого поставил подпись
- *IsValid* - признак того, что подпись либо еще не прошла проверку, либо проверена и признана верной
- :doc:`VerificationResult <SignatureVerificationResult>` - результат проверки подписи. Возвращается в ответе методов, если в запросе был установлен InjectEntityContent=true
- :doc:`DeliveredAt <Timestamp>` - метка времени доставки подписи
