SenderTitleDocflow
==================

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message SenderTitleDocflow
    {
        required bool IsFinished = 1;
        required SignedAttachmentV3 Attachment = 2;
        optional Timestamp SentAt = 3;
        optional Timestamp DeliveredAt = 4;
        optional RoamingNotification RoamingNotification = 5;
        required Documents.SenderSignatureStatus SenderSignatureStatus = 6;
    }

Структура содержит информацию о состоянии титула отправителя. Содержится в структуре :doc:`DocflowV3`.

- *IsFinished* - признак того, что документооборот по титулу отправителя завершен, т. е. не требует дальнейших действий
- :doc:`Attachment <SignedAttachmentV3>` - данные о файле титула отправителя и подписи под ним
- :doc:`SentAt <Timestamp>` - метка времени отправки титула отправителя
- :doc:`DeliveredAt <Timestamp>` - метка времени доставки титула отправителя в ящик получателя
- :doc:`RoamingNotification` - данные о доставке документа в роуминг
- :doc:`SenderSignatureStatus` - статус подписи отправителя