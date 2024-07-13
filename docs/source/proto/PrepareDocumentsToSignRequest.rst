PrepareDocumentsToSignRequest
=============================

Структура ``PrepareDocumentsToSignRequest`` представляет собой запрос на подготовку документов к подписанию.

.. code-block:: protobuf

    message PrepareDocumentsToSignRequest {
        required string BoxId = 1;
        repeated DraftDocumentToPatch DraftDocuments = 2;
        repeated DocumentToPatch Documents = 3;
        repeated ContentToPatch Contents = 4;
    }

    message DraftDocumentToPatch {
        required DocumentId DocumentId = 1;
        optional string ToBoxId = 2;
        optional Signer Signer = 3;
        repeated ExtendedSigner ExtendedSigner = 4;
        optional bytes SignerContent = 5;
    }

    message DocumentToPatch {
        required DocumentId DocumentId = 1;
        optional Signer Signer = 2;
        repeated ExtendedSigner ExtendedSigner = 3;
        optional bytes SignerContent = 4;
    }

    message ContentToPatch {
        required string TypeNamedId = 1;
        required string Function = 2;
        required string Version = 3;
        required UnsignedContent Content = 4;
        optional string ToBoxId = 5;
        optional Signer Signer = 6;
        repeated ExtendedSigner ExtendedSigner = 7;
        optional bytes SignerContent = 8;
    }

- ``BoxId`` — идентификатор ящика, документы из которого нужно подготовить к подписанию.
- ``DraftDocuments`` — список черновиков документов, которые нужно подготовить к подписанию. Отправить подготовленные черновики можно с помощью метода :doc:`../http/SendDraft`. Каждый элемент списка представлен структурой ``DraftDocumentToPatch`` с полями:

	- ``DocumentId`` — идентификатор черновика документа, который нужно подготовить к подписанию и отправке. Представлен структурой :doc:`DocumentId`.
	- ``ToBoxId`` — идентификатор ящика, в который нужно отправить документ. Если поле не задано, используется идентификатор ящика получателя из черновика.

	.. include:: ../include/desc_signers.txt

- ``Documents`` — список патчей документов, которые нужно подготовить к подписанию и отправке. Отправить подготовленные патчи можно с помощью метода :doc:`../http/PostMessagePatch`. Каждый элемент списка представлен структурой ``DocumentToPatch`` с полями:

	- ``DocumentId`` — идентификатор документа с :ref:`отложенной отправкой <doc_delaysend>`, который нужно подготовить к подписанию. Представлен структурой :doc:`DocumentId`.

	.. include:: ../include/desc_signers.txt

- ``Contents`` — список документов, которые нужно подготовить к подписанию и отправке. Отправить документы можно с помощью метода :doc:`../http/PostMessage`. Каждый элемент списка представлен структурой ``ContentToPatch`` с полями:

	- ``TypeNamedId`` — идентификатор типа документа.
	- ``Function`` — функция документа.
	- ``Version`` — версия документа.
	- ``Content`` — содержимое документа, представленное структурой :doc:`UnsignedContent`.
	- ``ToBoxId`` — идентификатор ящика, в который нужно отправить документ. Если поле не задано, используется идентификатор ящика получателя из документа.

	.. include:: ../include/desc_signers.txt


----

.. rubric:: См. также

*Инструкции:*
	- :doc:`../instructions/preparetosign`

*Структура используется:*
	- в теле запроса метода :doc:`../http/PrepareDocumentsToSign`

*Методы для работы с подготовленными к подписанию документами:*
	- :doc:`../http/PostMessage` — отправляет сообщение
	- :doc:`../http/PostMessagePatch` — отправляет дополнение к сообщению
	- :doc:`../http/SendDraft` — отправляет сообщение, созданное из черновика