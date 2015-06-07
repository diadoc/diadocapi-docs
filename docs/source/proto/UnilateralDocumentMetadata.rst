UnilateralDocumentMetadata
==========================

.. code-block:: protobuf

    message ProformaInvoiceMetadata {
        optional UnilateralDocumentStatus DocumentStatus = 1 [default = UnknownUnilateralDocumentStatus];
        required string Total = 2;
        optional string Vat = 3;
        optional string Grounds = 4;
    }

    message ServiceDetailsMetadata {
        optional UnilateralDocumentStatus DocumentStatus = 1 [default = UnknownUnilateralDocumentStatus];
    }

    enum UnilateralDocumentStatus {
        UnknownUnilateralDocumentStatus = 0;
        Outbound = 1;
        OutboundWaitingForSenderSignature = 4;
        OutboundInvalidSenderSignature = 5;
        Inbound = 2;
        Internal = 3;
        InternalWaitingForSenderSignature = 6;
        InternalInvalidSenderSignature = 7;
    }
        

Структура ProformaInvoiceMetadata содержит дополнительные атрибуты документа (в структуре :doc:`Document`) специфичные для счетов на оплату:

-  DocumentStatus определяет состояние, в котором находится данный документ; принимает одно из значений перечисления UnilateralDocumentStatus.

-  Total - сумма счета.

-  Vat - сумма НДС счета; если поле не заполнено, это значит что счет был создан с отметкой "без НДС".

-  Grounds - основания для счета; представляются в виде неформализованной строки текста, например, "Договор №1234, Заказ №321".

Структура ServiceDetailsMetadata содержит дополнительные атрибуты документа (в структуре :doc:`Document`) специфичные для счетов на оплату:

-  DocumentStatus определяет состояние, в котором находится данный документ; принимает одно из значений перечисления UnilateralDocumentStatus.

Перечисление UnilateralDocumentStatus задает возможные варианты состояний, в которых может находиться односторонний документ (например, счет на оплату):

-  UnknownUnilateralDocumentStatus (неизвестное состояние; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать состояние документа, переданное сервером),
-  Outbound (документ исходящий),
-  OutboundWaitingForSenderSignature (документ исходящий, документ не отправлен, поскольку не подписан отправителем),
-  OutboundInvalidSenderSignature (документ исходящий, документ не отправлен, поскольку подпись отправителя не является корректной),
-  Inbound (документ входящий).
-  Internal (документ внутренний).
-  InternalWaitingForSenderSignature (документ внутренний, документ не отправлен, поскольку не подписан отправителем),
-  InternalInvalidSenderSignature (документ внутренний, документ не отправлен, поскольку подпись отправителя не является корректной),