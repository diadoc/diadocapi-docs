ReceiptGenerationRequestV2
==========================

Структура ``ReceiptGenerationRequestV2`` представляет собой исходные данные подписанта для формирования извещения о получении (ИоП).

.. code-block:: protobuf

    message ReceiptGenerationRequestV2 {
        required string MessageId = 1;
        required string AttachmentId = 2;
        required bytes SignerContent = 3;
    }

- ``MessageId`` — идентификатор сообщения.
- ``AttachmentId`` — идентификатор :doc:`сущности <../proto/Entity message>`, для которой нужно сформировать ИоП.
- ``SignerContent`` — бинарное представление xml-файла универсального подписанта. Файл формируется в соответствии с :download:`XSD-схемой <../xsd/TechnologicalSigner133UserContract1505.xsd>`.