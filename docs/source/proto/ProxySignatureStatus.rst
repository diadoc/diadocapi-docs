ProxySignatureStatus
=====================

.. code-block:: protobuf

    enum ProxySignatureStatus {
        UnknownProxySignatureStatus = 0;
        ProxySignatureStatusNone = 1;
        WaitingForProxySignature = 2;
        WithProxySignature = 3;
        ProxySignatureRejected = 4;
        InvalidProxySignature = 5;
    }

Перечисление отражает статус промежуточной подписи. Возможные значения:

  - *UnknownProxySignatureStatus* - неизвестный статус промежуточной подписи; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать статус промежуточной подписи, переданный сервером;
  - *ProxySignatureStatusNone* - документ не требует промежуточной подписи;
  - *WaitingForProxySignature* - ожидается промежуточная подпись;
  - *WithProxySignature* - промежуточная подпись проверена и валидна;
  - *ProxySignatureRejected* - промежуточный получатель отказал в подписи;
  - *InvalidProxySignature* - промежуточная подпись проверена и невалидна.