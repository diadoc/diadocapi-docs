RevocationRequestInfo
=====================

.. code-block:: protobuf

    message RevocationRequestInfo {
        optional string Comment = 1;
        optional Signer Signer = 2;
    }
        

Структура данных RevocationRequestInfo представляет исходные данные для формирования предложения об аннулировании документа при помощи метода :doc:`../http/GenerateRevocationRequestXml`:

-  Comment - необязательный текст комментария к предложению об аннулировании документа.

-  Signer - необязательная информация о подписанте предложения в виде структуры данных :doc:`Signer`.