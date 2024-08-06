EncryptedDocumentMetadata
=========================

.. warning::
	Структура устарела.

Структура ``EncryptedDocumentMetadata`` представляет собой метаднные зашифрованного документа в отправляемом сообщении.

.. code-block:: protobuf

    message EncryptedDocumentMetadata {
        required string FileId = 1;
        required string BuyerFnsParticipantId = 2;
        required string SenderFnsParticipantId = 3;
        required DocumentDateAndNumber DocumentDateAndNumber = 4;
    }

- ``FileId`` — строковый идентификатор файла.
- ``BuyerFnsParticipantId`` — идентифиткатор участника ЭДО покупателя.
- ``SenderFnsParticipantId`` — идентифиткатор участника ЭДО продавца.
- ``DocumentDateAndNumber`` — дата и номер документа, представленные структурой :doc:`DocumentDateAndNumber`.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`EncryptedInvoiceAttachment`
	- в устаревшей структуре :doc:`EncryptedXmlDocumentAttachment`