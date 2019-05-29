OrganizationFeatures
====================

.. code-block:: protobuf

    message OrganizationFeatures
    {
        required BlockStatus BlockStatus = 1;
        repeated string Features = 2;
    }

Структура *OrganizationFeatures* содержит информацию о статусе блокировки ящика на отправку документов и о включенных дополнительных функциях.

- :doc:`BlockStatus <BlockStatus>` - статус блокировки ящика на отправку документов.
- *Features* - список включенных дополнительных функций ящика

    + AllowApprovementSignatures - согласующая подпись
    + AllowDocumentsForwarding - пересылка документов третьей стороне
    + AllowProxifiedDocuments - отправка документов через промежуточного получателя
    + AllowSendEncryptedDocuments - отправка зашифрованных документов
