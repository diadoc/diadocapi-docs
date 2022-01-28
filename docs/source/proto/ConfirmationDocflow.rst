ConfirmationDocflow
===================

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message ConfirmationDocflow
    {
        required bool IsFinished = 1;
        optional SignedAttachmentV3 ConfirmationAttachment = 2;
        optional Timestamp ConfirmedAt = 3;
        optional ReceiptDocflowV3 Receipt = 4;
        optional OperatorConfirmationDocflow RoamingConfirmation = 5;
    }

Структура содержит информацию о состоянии подтверждения даты доставки, которое формирует оператор ЭДО. Содержится в структуре :doc:`DocflowV3`.

- ``IsFinished`` — признак того, что документооборот по подтверждении оператора завершен, т. е. не требует дальнейших действий
- :doc:`ConfirmationAttachment <SignedAttachmentV3>` — данные о файле подтверждения оператора и подписи под ним
- :doc:`ConfirmedAt <Timestamp>` — дата подтверждения оператора
- :doc:`Receipt <ReceiptDocflowV3>` — информация об извещении о получении подтверждения оператора
- :doc:`RoamingConfirmation <OperatorConfirmationDocflow>` — информация о подтверждении роумингового оператора