RecipientResponseStatus
=======================

Отвечает за состояние ответного действия со стороны получателя документа. Под ответным действием имеет ввиду подпись под документом либо отправка ответного титула.

Контракт:

.. code-block:: protobuf

    enum RecipientResponseStatus {
        RecipientResponseStatusUnknown = 0;
        RecipientResponseStatusNotAcceptable = 1;
        WaitingForRecipientSignature = 2;
        WithRecipientSignature = 3;
        RecipientSignatureRequestRejected = 4;
        InvalidRecipientSignature = 5;
        WithRecipientPartiallySignature = 6
    }

Расшифровка значений:

- *RecipientResponseStatusNotAcceptable* - ответного действия не требуется. Либо это т.н. односторонний документ, например, счет, либо счет-фактура и УПД СЧФ, либо документ с опциональным запросом подписи, которая не была запрошена. Сюда также подходит однотитульный акт (*XmlAcceptanceCertificate*).

- *WaitingForRecipientSignature* - ожидается ответное действие получателя документа. Если документ исходящий, то не требует никаких действия. Если входящий - требуется либо подписать документ (ответный титул), либо отказать в подписи.

- *WithRecipientSignature* - получатель подписал документ (ответный титул).

- *RecipientSignatureRequestRejected* - получатель документа отказал в подписи.

- *InvalidRecipientSignature* — получатель подписал документ невалидной подписью. Если это незашифрованный документ, то такой статус возможен только на стороне получателя документа.

- *WithRecipientPartiallySignature* - получатель подписал документ (ответный титул) с разногласиями. 
