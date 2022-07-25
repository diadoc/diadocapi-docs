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
- ``RevocationStatusNone`` — документ не аннулирован и не было предложений об аннулировании. Может возвращаться в случае если по документу сформирован запрос на аннулирование, но он еще не отправлен (например, находится на согласовании на стороне отправителя).
- ``RevocationIsRequestedByMe`` — отправлено исходящее предложение об аннулировании документа.
- ``RequestsMyRevocation`` — получено входящее предложение об аннулировании документа.
- ``RevocationAccepted`` — документ аннулирован.
- ``RevocationRejected`` — получен или отправлен отказ от предложения об аннулировании документа.

----

Смотри также
^^^^^^^^^^^^

Перечисление используется:
	- в структуре :doc:`RevocationDocflowV3`,
	- в структуре :doc:`Document`.