ProxyResponseDocflow
====================

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message ProxyResponseDocflow
    {
        required bool IsFinished = 1;
        optional SignatureV3 Signature = 2;
        optional SignatureRejectionDocflow Rejection = 3;
        required Documents.ProxySignatureStatus ProxySignatureStatus = 4;
    }

Структура содержит информацию об ответе от промежуточного получателя. Содержится в структуре :doc:`DocflowV3`.

- *IsFinished* - признак того, что документооборот по ответу от промежуточного получателя завершен, т. е. не требует дальнейших действий
- :doc:`Signature <SignatureV3>` - данные о файле подписи промежуточного получателя
- :doc:`Rejection <SignatureRejectionDocflow>` - данные об отказе в подписи промежуточного получателя
- :doc:`ProxySignatureStatus` - статус подписи промежуточного получателя
