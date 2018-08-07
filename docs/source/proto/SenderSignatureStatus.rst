SenderSignatureStatus
=====================

.. code-block:: protobuf

    enum SenderSignatureStatus {
        UnknownSenderSignatureStatus = 0;
        WaitingForSenderSignature = 1;
        SenderSignatureUnchecked = 2;
        SenderSignatureCheckedAndValid = 3;
        SenderSignatureCheckedAndInvalid = 4;
    }

Перечисление отражает статус подписи отправителя:

- *UnknownSenderSignatureStatus* - значение зарезервировано для устаревших клиентов;
- *WaitingForSenderSignature* - ожидается подпись отправителя;
- *SenderSignatureUnchecked* - подпись отправителя еще не проверена;
- *SenderSignatureCheckedAndValid* - подпись отправителя проверена и валидна;
- *SenderSignatureCheckedAndInvalid* - подпись отправителя проверена и невалидна.