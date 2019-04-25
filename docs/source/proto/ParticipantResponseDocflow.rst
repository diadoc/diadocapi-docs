ParticipantResponseDocflow
==========================

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message ParticipantResponseDocflow
    {
        required bool IsFinished = 1;
        optional SignatureV3 Signature = 2;
        optional SignedAttachmentV3 Title = 3;
        optional SignatureRejectionDocflow Rejection = 4;
        optional Timestamp SentAt = 5;
        optional Timestamp DeliveredAt = 6;
        required Documents.RecipientResponseStatus ResponseStatus = 7;
    }

Структура содержит информацию о состоянии ответного действия участника документооборота. Содержится в структуре :doc:`DocflowV3`.

- *IsFinished* - признак того, что документооборот по ответному действию завершен, т. е. не требует дальнейших действий со стороны участника документооборота
- :doc:`Signature <SignatureV3>` - данные о файле подписи участника документооборота
- :doc:`Title <SignedAttachmentV3>` - данные о файле титула участника документооборота и подписи под ним
- :doc:`Rejection <SignatureRejectionDocflow>` - данные об отказе в подписи участника документооборота
- :doc:`SentAt <Timestamp>` - метка времени отправки ответа участника документооборота
- :doc:`DeliveredAt <Timestamp>` - метка времени доставки ответа участника документооборота в ящик отправителя
- :doc:`ResponseStatus <RecipientResponseStatus>` - статус ответа участника документооборота
