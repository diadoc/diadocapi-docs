AmendmentRequestMetadata
========================

Контракт, описывающий состояние уведомления об уточнении (УОУ). Актуален, например, для СФ и УПД, а также некоторых версий формализованных актов и накладных.

Описание:

.. code-block:: protobuf

    message AmendmentRequestMetadata {
        required int32 AmendmentFlags = 1;
        required GeneralReceiptStatus ReceiptStatus = 2;
    }

- :doc:`AmendmentFlags <InvoiceAmendmentFlags>` отражает статус УОУ:

    - было ли затребовано уточнение, передавалось ли исправление документа, передавалась ли корректировка документа;

    - представляет собой битовую маску, составленную из одного или нескольких значений перечисления :doc:`InvoiceAmendmentFlags`.

- :doc:`ReceiptStatus <GeneralReceiptStatus>` - статус извещения о получении под УОУ со стороны отправителя документа.