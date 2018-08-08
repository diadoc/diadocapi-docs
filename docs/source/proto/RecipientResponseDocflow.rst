RecipientResponseDocflow
========================

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message RecipientResponseDocflow
    {
        required bool IsFinished = 1;
        optional SignatureV3 Signature = 2;
        optional SignedAttachmentV3 RecipientTitle = 3;
        optional SignatureRejectionDocflow Rejection = 4;
        optional Timestamp SentAt = 5;
        optional Timestamp DeliveredAt = 6;
        required Documents.RecipientResponseStatus RecipientResponseStatus = 7;
    }

Структура содержит информацию о состоянии ответного действия получателя. Содержится в структуре :doc:`DocflowV3`.

- *IsFinished* - признак того, что документооборот по ответному действию завершен, т. е. не требует дальнейших действий со стороны получателя документа
- :doc:`Signature <SignatureV3>` - данные о файле подписи получателя
- :doc:`RecipientTitle <SignedAttachmentV3>` - данные о файле титула получателя и подписи под ним
- :doc:`Rejection <SignatureRejectionDocflow>` - данные об отказе в подписи получателя
- :doc:`SentAt <Timestamp>` - метка времени отправки ответа получателя
- :doc:`DeliveredAt <Timestamp>` - метка времени доставки ответа получателя в ящик отправителя
- :doc:`RecipientResponseStatus` - статус ответа получателя
