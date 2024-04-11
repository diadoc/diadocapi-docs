RevocationStatus
================

Перечисление ``RevocationStatus`` представляет собой статус аннулирования документа.

.. code-block:: protobuf

    enum RevocationStatus {
        UnknownRevocationStatus = 0;
        RevocationStatusNone = 1;
        RevocationIsRequestedByMe = 2;
        RequestsMyRevocation = 3;
        RevocationAccepted = 4;
        RevocationRejected = 5;
    }

- ``UnknownRevocationStatus`` — неизвестный статус. Возвращается только в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать статус аннулирования документа, переданный сервером.
- ``RevocationStatusNone`` — документ не аннулирован. Возвращается в следующих случаях:

	- по документу не было предложения об аннулировании;
	- может возвращаться отправителю, если по документу сформирован, но еще не отправлен запрос на аннулирование (например, находится на согласовании на стороне отправителя).

- ``RevocationIsRequestedByMe`` — отправлено исходящее предложение об аннулировании документа.
- ``RequestsMyRevocation`` — получено входящее предложение об аннулировании документа.
- ``RevocationAccepted`` — документ аннулирован.
- ``RevocationRejected`` — получен или отправлен отказ от предложения об аннулировании документа.

----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`Document`
	- в структуре :doc:`RevocationDocflowV3`