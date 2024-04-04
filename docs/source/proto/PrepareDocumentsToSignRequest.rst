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
        optional Invoicing.Signer Signer = 6;
        repeated Invoicing.Signers.ExtendedSigner ExtendedSigner = 7;
        optional bytes SignerContent = 8;
    }

- ``BoxId`` — идентификатор ящика, документы из которого нужно подготовить к подписанию.
- ``DraftDocuments`` — список черновиков документов, которые нужно подготовить к подписанию. Отправить черновики можно с помощью метода :doc:`../http/SendDraft`. Каждый элемент списка представлен структурой ``DraftDocumentToPatch`` с полями:

	- ``DocumentId`` — идентификатор черновика документа, который нужно подготовить к подписанию и отправке. Представлен структурой :doc:`DocumentId`.

	- ``ToBoxId`` — идентификатор ящика, в адрес которого нужно отправить документ. Если поле не задано, используется идентификатор ящика получателя из черновика.

	- ``Signer`` — информация о подписанте документа. Представлена структурой :doc:`Signer`. Структуру ``Signer`` нельзя использовать для документов в формате УПД. Если при подписании документов форматов :doc:`@93/@172 <../docflows/AttachmentVersion>` поле ``Signer`` не задано, то будут указаны ФИО и должность пользователя, вызывающего метод.

	- ``ExtendedSigner`` — информация о подписанте документа. Представлена структурой :doc:`utd/ExtendedSigner`. Если у документа больше одного подписанта, вернется ошибка ``400 (Bad Request)``. Используется для документов форматов :doc:`@155/@189/@551/@552/@736/@820 <../docflows/AttachmentVersion>` и своих типов на базе форматов :doc:`@155/@820 <../docflows/AttachmentVersion>`.

	- ``SignerContent`` — бинарное представление упрощенного XML-файла подписанта. XSD-схему можно получить с помощью метода :doc:`../http/GetDocumentTypes`. Ссылка на XSD-схему упрощенного XML подписанта вернется в поле ``SignerUserDataXsdUrl``.

- ``Documents`` — список патчей документов, которые нужно подготовить к подписанию и отправке. Отправить патчи можно с помощью метода :doc:`../http/PostMessagePatch`. Каждый элемент списка представлен структурой ``DocumentToPatch`` с полями:

	- ``DocumentId`` — идентификатор документа с :ref:`отложенной отправкой<doc_delaysend>`, который нужно подготовить к подписанию. Представлен структурой :doc:`DocumentId`.

	- ``Signer`` — информация о подписанте документа. Представлена структурой :doc:`Signer`. Структуру ``Signer`` нельзя использовать для документов в формате УПД. Если при подписании документов форматов :doc:`@93/@172 <../docflows/AttachmentVersion>` поле ``Signer`` не задано, то будут указаны ФИО и должность пользователя, вызывающего метод.

	- ``ExtendedSigner`` — информация о подписанте документа. Представлена структурой :doc:`utd/ExtendedSigner`. Если у документа больше одного подписанта, вернется ошибка ``400 (Bad Request)``. Используется для документов форматов :doc:`@155/@189/@551/@552/@736/@820 <../docflows/AttachmentVersion>` и своих типов на базе форматов :doc:`@155/@820 <../docflows/AttachmentVersion>`.

	- ``SignerContent`` — бинарное представление упрощенного XML-файла подписанта. XSD-схему можно получить с помощью метода :doc:`../http/GetDocumentTypes`. Ссылка на XSD-схему упрощенного XML подписанта вернется в поле ``SignerUserDataXsdUrl``.

- ``Contents`` — список документов, которые нужно подготовить к подписанию и отправке. Отправить документы можно с помощью метода :doc:`../http/PostMessage`. Каждый элемент списка представлен структурой ``ContentToPatch`` с полями:

	- ``TypeNamedId`` — идентификатор типа документа.

	- ``Function`` — функция документа.

	- ``Version`` — версия документа.

	- ``Content`` — содержимое документа. Представлено структурой :doc:`UnsignedContent`.

	- ``ToBoxId`` — идентификатор ящика, в адрес которого нужно отправить документ. Если поле не задано, используется идентификатор ящика получателя из документа.

	- ``Signer`` — информация о подписанте документа. Представлена структурой :doc:`Signer`. Структуру ``Signer`` нельзя использовать для документов в формате УПД. Если при подписании документов форматов :doc:`@93/@172 <../docflows/AttachmentVersion>` поле ``Signer`` не задано, то будут указаны ФИО и должность пользователя, вызывающего метод.

	- ``ExtendedSigner`` — информация о подписанте документа. Представлена структурой :doc:`utd/ExtendedSigner`. Если у документа больше одного подписанта, вернется ошибка ``400 (Bad Request)``. Используется для документов форматов :doc:`@155/@189/@551/@552/@736/@820 <../docflows/AttachmentVersion>` и своих типов на базе форматов :doc:`@155/@820 <../docflows/AttachmentVersion>`.

	- ``SignerContent`` — бинарное представление упрощенного XML-файла подписанта. XSD-схему можно получить с помощью метода :doc:`../http/GetDocumentTypes`. Ссылка на XSD-схему упрощенного XML подписанта вернется в поле ``SignerUserDataXsdUrl``.

----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/PrepareDocumentsToSign`