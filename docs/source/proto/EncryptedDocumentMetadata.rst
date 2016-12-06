EncryptedDocumentMetadata
=========================

.. code-block:: protobuf

    message EncryptedDocumentMetadata {
	    required string FileId = 1;
	    required string BuyerFnsParticipantId = 2;
	    required string SenderFnsParticipantId = 3;
	    required DocumentDateAndNumber DocumentDateAndNumber = 4;
    }



Структура данных *EncryptedDocumentMetadata* представляет метаднные зашифрованного документа в отправляемом сообщении :doc:`MessageToPost`:

-  *FileId* - идентификатор файла, представленный в виде строки.

-  *BuyerFnsParticipantId* - идентифиткатор участника ЭДО покупателя.

-  *SenderFnsParticipantId* - идентифиткатор участника ЭДО продавца.

-  *DocumentDateAndNumber* - дата и номер счета-фактуры, представленные в виде структуры :doc:`DocumentDateAndNumber`.
