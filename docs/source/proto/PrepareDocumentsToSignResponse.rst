PrepareDocumentsToSignResponse
==============================

Структура ``PrepareDocumentsToSignResponse`` представляет собой документы, подготовленные к подписанию и отправке методом :doc:`../http/PrepareDocumentsToSign`.

.. code-block:: protobuf

    message PrepareDocumentsToSignResponse {
        repeated DocumentPatchedContent DocumentPatchedContents = 1;
    }

    message DocumentPatchedContent {
        required DocumentId DocumentId = 1;
        required string PatchedContentId = 2;
        optional bytes Content = 3;
    }

- ``DocumentPatchedContents`` — список документов, подготовленных к подписанию и отправке. Каждый элемент списка представлен структурой ``DocumentPatchedContent`` с полями:

	- ``DocumentId`` — идентификатор документа, подготовленного к подписанию и отправке, представленный структурой :doc:`DocumentId`.
	- ``PatchedContentId`` — идентификатор содержимого документа, подготовленного к подписанию и отправке. Идентификатор можно использовать при вызове метода :doc:`../http/SendDraft` в поле ``PatchedContentId`` структуры :doc:`DocumentSenderSignature`.
	- ``Content`` — подготовленное к подписанию содержимое документа. Подпись под документом нужно формировать для этого содержимого.

----

.. rubric:: См. также

*Инструкции:*
	- :doc:`../instructions/preparetosign`

*Структура используется:*
	- в теле ответа метода :doc:`../http/PrepareDocumentsToSign`

*Методы для работы с подготовленными к подписанию документами:*
	- :doc:`../http/PostMessage` — отправляет сообщение
	- :doc:`../http/PostMessagePatch` — отправляет дополнение к сообщению
	- :doc:`../http/SendDraft` — отправляет сообщение, созданное из черновика