ConfirmationDocflow
===================

.. code-block:: protobuf

    message ConfirmationDocflow
    {
        required bool IsFinished = 1;
        optional SignedAttachmentV3 ConfirmationAttachment = 2;
        optional Timestamp ConfirmedAt = 3;
        optional ReceiptDocflowV3 Receipt = 4;
        optional OperatorConfirmationDocflow RoamingConfirmation = 5;
    }

Структура содержит информацию о состоянии подтверждения даты доставки, которое формирует оператор ЭДО.

- ``IsFinished`` — признак того, что документооборот по подтверждении оператора завершен, т. е. не требует дальнейших действий.
- ``ConfirmationAttachment`` — данные о файле подтверждения оператора и подписи под ним, представленные структурой :doc:`SignedAttachmentV3`.
- ``ConfirmedAt`` — дата подтверждения оператора, представленная структурой :doc:`Timestamp`.
- ``Receipt`` — информация об извещении о получении подтверждения оператора, представленная структурой :doc:`ReceiptDocflowV3`.
- ``RoamingConfirmation`` — подтверждение оператора, отправленное в роуминг или полученное из роуминга, представленное структурой :doc:`OperatorConfirmationDocflow`.

----

.. rubric:: Использование

Структура ``ConfirmationDocflow`` используется в структуре :doc:`DocflowV3`.