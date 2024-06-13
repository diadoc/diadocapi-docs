SignatureRejectionGenerationRequestV2
=====================================

Структура ``SignatureRejectionGenerationRequestV2`` представляет собой исходные данные для формирования файла отказа от подписи документа или отказа от предложения об аннулировании документа.

.. code-block:: protobuf

    message SignatureRejectionGenerationRequestV2 {
        optional string ErrorMessage = 1;
        required string MessageId = 2;
        required string AttachmentId = 3;
        required bytes SignerContent = 4;
    }

- ``ErrorMessage`` — необязательный текст комментария к отказу. Максимально допустимая длина 5000 символов.
- ``MessageId`` — идентификатор сообщения.
- ``AttachmentId`` — идентификатор :doc:`сущности <../proto/Entity message>`, для которой требуется сформировать файл отказа от подписи.
- ``SignerContent`` — бинарное представление XML-файла универсального подписанта. Файл формируется в соответствии с :download:`XSD-схемой <../xsd/TechnologicalSigner133UserContract1505.xsd>`. Подробнее о формировании файла в разделе :ref:`universal_signer`.