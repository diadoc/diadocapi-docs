InvoiceCorrectionRequestGenerationRequestV2
===========================================

Структура ``InvoiceCorrectionRequestGenerationRequestV2`` представляет собой исходные данные для формирования уведомления об уточнении счета-фактуры.

.. code-block:: protobuf

    message InvoiceCorrectionRequestGenerationRequestV2 {
        required string ErrorMessage = 1;
        required string MessageId = 2;
        required string AttachmentId = 3;
        required bytes SignerContent = 4;
    }

- ``ErrorMessage`` — обязательный текст уведомления об уточнении. Максимально допустимая длина 20000 символов.
- ``MessageId`` — идентификатор сообщения.
- ``AttachmentId`` — идентификатор сущности СФ/ИСФ/КСФ/ИКСФ, для которой нужно сформировать уведомление об уточнении.
- ``SignerContent`` — бинарное представление XML-файла универсального подписанта. Файл формируется в соответствии с :download:`XSD-схемой <../xsd/TechnologicalSigner133UserContract1505.xsd>`. Подробнее о формировании файла в разделе :ref:`universal_signer`.