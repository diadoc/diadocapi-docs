NonformalizedDocumentMetadata
=============================

.. code-block:: protobuf

    message NonformalizedDocumentMetadata {
        optional NonformalizedDocumentStatus DocumentStatus = 1 [default = UnknownNonformalizedDocumentStatus];
    }

    enum NonformalizedDocumentStatus {
        UnknownNonformalizedDocumentStatus = 0;
        OutboundNoRecipientSignatureRequest = 1;
        OutboundWaitingForRecipientSignature = 2;
        OutboundWithRecipientSignature = 3;
        OutboundRecipientSignatureRequestRejected = 4;
        OutboundWaitingForSenderSignature = 13;
        OutboundInvalidSenderSignature = 14;
        InboundNoRecipientSignatureRequest = 5;
        InboundWaitingForRecipientSignature = 6;
        InboundWithRecipientSignature = 7;
        InboundRecipientSignatureRequestRejected = 8;
        InboundInvalidRecipientSignature = 15;
        InternalNoRecipientSignatureRequest = 9;
        InternalWaitingForRecipientSignature = 10;
        InternalWithRecipientSignature = 11;
        InternalRecipientSignatureRequestRejected = 12;
        InternalWaitingForSenderSignature = 16;
        InternalInvalidSenderSignature = 17;
        InternalInvalidRecipientSignature = 18;
    }
        

Структура данных NonformalizedDocumentMetadata содержит дополнительные атрибуты документа (в структуре :doc:`Document`) специфичные для неформализованных документов:

-  DocumentStatus определяет состояние, в котором находится данный документ; возможные варианты:

   -  UnknownNonformalizedDocumentStatus (неизвестный статус; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать статус документа, переданный сервером),
   -  OutboundNoRecipientSignatureRequest (документ исходящий, без запроса ответной подписи),
   -  OutboundWaitingForRecipientSignature (документ исходящий, ответная подпись, либо отказ от ее формирования еще не получены),
   -  OutboundWithRecipientSignature (документ исходящий, ответная подпись получена),
   -  OutboundRecipientSignatureRequestRejected (документ исходящий, получен отказ от формирования ответной подписи),
   -  OutboundWaitingForSenderSignature (документ исходящий, документ не отправлен, поскольку не подписан отправителем),
   -  OutboundInvalidSenderSignature (документ исходящий, документ не отправлен, поскольку подпись отправителя не является корректной),
   -  InboundNoRecipientSignatureRequest (документ входящий, без запроса ответной подписи),
   -  InboundWaitingForRecipientSignature (документ входящий, ответная подпись, либо отказ от ее формирования еще не отправлены),
   -  InboundWithRecipientSignature (документ входящий, ответная подпись поставлена),
   -  InboundRecipientSignatureRequestRejected (документ входящий, отправлен отказ от формирования ответной подписи).
   -  InboundInvalidRecipientSignature (документ входящий, документооборот не завершен, поскольку подпись получателя не является корректной),
   -  InternalNoRecipientSignatureRequest (документ внутренний, без запроса ответной подписи),
   -  InternalWaitingForRecipientSignature (документ внутренний, ответная подпись, либо отказ от ее формирования еще не отправлены),
   -  InternalWithRecipientSignature (документ внутренний, ответная подпись поставлена),
   -  InternalRecipientSignatureRequestRejected (документ внутренний, отправлен отказ от формирования ответной подписи),
   -  InternalWaitingForSenderSignature (документ внутренний, документ не отправлен, поскольку не подписан отправителем),
   -  InternalInvalidSenderSignature (документ внутренний, документ не отправлен, поскольку подпись отправителя не является корректной),
   -  InternalInvalidRecipientSignature (документ внутренний, документооборот не завершен, поскольку подпись получателя не является корректной).