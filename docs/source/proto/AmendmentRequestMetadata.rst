AmendmentRequestMetadata
========================

Структура ``AmendmentRequestMetadata`` описывает состояние уведомления об уточнении (УоУ).

Используется для СФ, УПД и для некоторых версий формализованных актов и накладных.

.. code-block:: protobuf

    message AmendmentRequestMetadata {
        required int32 AmendmentFlags = 1;
        required GeneralReceiptStatus ReceiptStatus = 2;
    }

- ``AmendmentFlags`` — статус УОУ. Указывает, было ли затребовано уточнение, передавалось ли исправление документа, передавалась ли корректировка документа. Представляет собой битовую маску, составленную из одного или нескольких значений перечисления :doc:`InvoiceAmendmentFlags`.
- ``ReceiptStatus`` — статус извещения о получении под УОУ со стороны отправителя документа, представленный структурой :doc:`GeneralReceiptStatus`.


----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`Document`.