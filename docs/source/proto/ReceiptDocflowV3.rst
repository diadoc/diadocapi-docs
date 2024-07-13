ReceiptDocflowV3
================

.. code-block:: protobuf

    message ReceiptDocflowV3
    {
        required bool IsFinished = 1;
        optional SignedAttachmentV3 ReceiptAttachment = 2;
        optional Timestamp SentAt = 3;
        optional Timestamp DeliveredAt = 4;
        optional ConfirmationDocflow Confirmation = 5;
        required Documents.GeneralReceiptStatus Status = 6;
    }

Структура содержит информацию о состоянии извещения о получении.

- *IsFinished* - признак того, что документооборот по извещению о получении завершен, т. е. не требует дальнейших действий
- :doc:`ReceiptAttachment <SignedAttachmentV3>` - данные о файле извещения о получении и подписи под ним
- :doc:`SentAt <Timestamp>` - время отправки извещения о получении
- :doc:`DeliveredAt <Timestamp>` - время доставки извещения о получении
- :doc:`Confirmation <ConfirmationDocflow>` - информация о подтверждении оператором даты доставки извещения
- :doc:`GeneralReceiptStatus` - статус извещения о получении
