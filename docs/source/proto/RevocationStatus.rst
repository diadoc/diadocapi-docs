RevocationStatus
================

.. code-block:: protobuf

    enum RevocationStatus {
        UnknownRevocationStatus = 0;
        RevocationStatusNone = 1;
        RevocationIsRequestedByMe = 2;
        RequestsMyRevocation = 3;
        RevocationAccepted = 4;
        RevocationRejected = 5;
    }

Перечисление отражает статус аннулирования документа. Возможные значения:

-  *UnknownRevocationStatus* - неизвестный статус аннулирования документа; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать статус аннулирования документа, переданный сервером;
-  *RevocationStatusNone* - документ не аннулирован, и не было предложений об аннулировании. Возвращается в случае если по документу сформирован запрос на аннулирование, но он еще не отправлен, а например находится на согласовании на стороне отправителя;
-  *RevocationIsRequestedByMe* - отправлено исходящее предложение об аннулировании документа;
-  *RequestsMyRevocation* - получено входящее предложение об аннулировании документа;
-  *RevocationAccepted* - документ аннулирован;
-  *RevocationRejected* - получен или отправлен отказ от предложения об аннулировании документа.
