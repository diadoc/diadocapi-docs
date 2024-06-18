RecipientResponseStatus
=======================

Перечисление ``RecipientResponseStatus`` представляет собой состояние ответного действия со стороны получателя документа — подпись под документом или отправка ответного титула.

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

- ``RecipientResponseStatusNotAcceptable`` — ответное действие не требуется. Возвращается в структуре :doc:`Document` ответа метода :doc:`../http/GetDocument` в следующих случаях:

	- документ односторонний, например: счет, счет-фактура, УПД СЧФ,
	- документ с опциональным запросом подписи, которая не была запрошена,
	- документ — однотитульный акт (``XmlAcceptanceCertificate``).

- ``WaitingForRecipientSignature`` — ожидается ответное действие получателя документа. Если документ исходящий, то не требует никаких действия. Если входящий — требуется либо подписать документ (ответный титул), либо отказать в подписи.

- ``WithRecipientSignature`` — получатель подписал документ (ответный титул).

- ``RecipientSignatureRequestRejected`` — получатель документа отказал в подписи.

- ``InvalidRecipientSignature`` — получатель подписал документ невалидной подписью. Если это незашифрованный документ, то такой статус возможен только на стороне получателя документа.

- ``WithRecipientPartiallySignature`` — получатель подписал документ (ответный титул) с разногласиями.


----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`Document`
	- в структуре :doc:`ParticipantResponseDocflow`