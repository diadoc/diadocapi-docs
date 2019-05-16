OrganizationFeatures
====================

.. code-block:: protobuf

    message OrganizationFeatures
    {
        required BlockStatus BlockStatus = 1;
        repeated string Features = 2;
    }

Структура *OrganizationFeatures* содержит информацию о статусе блокировки и BoxFeatures ящика.

- :doc:`BlockStatus <BlockStatus>` - статус блокировки организации.
- *Features* - список включенных BoxFeatures ящика

    + AllowApprovementSignatures - разрешить согласующую подпись
    + AllowDocumentsForwarding - разрешить пересылку документов третьей стороне
    + AllowProxifiedDocuments - разрешить отправлять документы через промежуточного получателя
    + AllowSendEncryptedDocuments - разрешить посылать зашифрованные документы
