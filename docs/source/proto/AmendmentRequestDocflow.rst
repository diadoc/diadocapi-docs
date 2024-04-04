AmendmentRequestDocflow
=======================

Структура ``AmendmentRequestDocflow`` хранит информацию о состоянии уведомления об уточнении (УоУ).

.. code-block:: protobuf

    message AmendmentRequestDocflow
    {
        required bool IsFinished = 1;
        optional SignedAttachmentV3 AmendmentRequest = 2;
        optional Timestamp SentAt = 3;
        optional Timestamp DeliveredAt = 4;
        optional ReceiptDocflowV3 Receipt = 5;
        required int32 AmendmentFlags = 6;
        optional string PlainText = 7;
        optional ConfirmationDocflow ConfirmationDocflow = 8;
    }

- ``IsFinished`` — флаг указывающий, что документооборот по УоУ завершен и не требует дальнейших действий.
- ``AmendmentRequest`` — информация о файле УоУ и подписи под ним, представленная структурой :doc:`SignedAttachmentV3`.
- ``SentAt`` — метка времени отправки УоУ, представленная структурой :doc:`Timestamp`.
- ``DeliveredAt`` — метка времени доставки УоУ в ящик отправителя документа, представленная структурой :doc:`Timestamp`.
- ``Receipt`` — информация об извещении о получении УоУ отправителем документа, представленная структурой :doc:`ReceiptDocflowV3`.
- ``AmendmentFlags`` — статус УОУ, принимает значения из перечисления :doc:`InvoiceAmendmentFlags`.
- ``PlainText`` — текст уведомления об уточнении.
- ``ConfirmationDocflow`` — информация о подтверждении оператором даты получения или доставки УОУ, представленная структурой :doc:`ConfirmationDocflow`.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocflowV3`