ParticipantResponseDocflow
==========================

Структура ``ParticipantResponseDocflow`` хранит информацию о состоянии ответного действия участника документооборота.

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
        optional ConfirmationDocflow Confirmation = 8;
    }

- ``IsFinished`` — флаг, указывающий, что текущий документооборот завершен. От участника документооборота не требуются дополнительные действия.
- ``Signature`` — информация о файле подписи. Представлена структурой :doc:`SignatureV3`.
- ``Title`` — информация о файле титула и подписи под ним. Представлена структурой :doc:`SignedAttachmentV3`.
- ``Rejection`` — информация об отказе в подписи. Представлена структурой :doc:`SignatureRejectionDocflow`.
- ``SentAt`` — :doc:`метка времени <Timestamp>` отправки ответа.
- ``DeliveredAt`` — :doc:`метка времени <Timestamp>` доставки ответа в ящик отправителя.
- ``ResponseStatus`` — статус ответа, принимает значения из перечисления :doc:`RecipientResponseStatus`.
- ``Confirmation`` — информация о состоянии подтверждения даты доставки. Представлена структурой :doc:`ConfirmationDocflow`. Подтверждение может возвращаться на титул покупателя или отказ в подписи.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocflowV3`.