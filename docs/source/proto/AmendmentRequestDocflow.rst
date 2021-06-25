AmendmentRequestDocflow
=======================

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

Структура содержит информацию о состоянии уведомления об уточнении (УоУ). Содержится в структуре :doc:`DocflowV3`.

- *IsFinished* - признак того, что документооборот по УоУ завершен, т. е. не требует дальнейших действий
- :doc:`AmendmentRequest <SignedAttachmentV3>` - данные о файле УоУ и подписи под ним
- :doc:`SentAt <Timestamp>` - метка времени отправки УоУ
- :doc:`DeliveredAt <Timestamp>` - метка времени доставки УоУ в ящик отправителя документа
- :doc:`Receipt <ReceiptDocflowV3>` - информация об извещении о получении УоУ отправителем документа
- :doc:`AmendmentFlags <InvoiceAmendmentFlags>` отражает статус УОУ:
    - было ли затребовано уточнение, передавалось ли исправление документа, передавалась ли корректировка документа;
    - представляет собой битовую маску, составленную из одного или нескольких значений перечисления :doc:`InvoiceAmendmentFlags`.
- *PlainText* - текст уведомления об уточнении
- :doc:`ConfirmationDocflow <ConfirmationDocflow>` - информация о подтверждении оператором даты получения или доставки уведомления об уточнении
