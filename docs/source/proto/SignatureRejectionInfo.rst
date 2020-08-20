SignatureRejectionInfo
======================

.. code-block:: protobuf

    message SignatureRejectionInfo {
        optional string ErrorMessage = 1;
        required Signer Signer = 2;
    }
        

Структура данных *SignatureRejectionInfo* представляет исходные данные для формирования отказа от подписи документа, либо отказа от предложения об аннулировании документа.

Файл отказа формируется при помощи метода :doc:`../http/GenerateSignatureRejectionXml`:

-  *ErrorMessage* - необязательный текст комментария к отказу. Максимально допустимая длина - 5000 символов.

-  *Signer* - обязательная информация о подписанте отказа, представленная в виде структуры данных :doc:`Signer`.
