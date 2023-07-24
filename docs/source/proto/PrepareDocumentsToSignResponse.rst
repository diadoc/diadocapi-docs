PrepareDocumentsToSignResponse
==============================

Структура ``PrepareDocumentsToSignResponse`` представляет собой документы, подготовленные к подписанию и отправке.

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

	- ``DocumentId`` — идентификатор документа, подготовленного к подписанию и отправке. Представлен структурой :doc:`DocumentId`.

	- ``PatchedContentId`` — идентификатор содержимого документа, подготовленного к подписанию и отправке. Идентификатор можно использовать при вызове метода :doc:`../http/SendDraft` в поле ``PatchedContentId`` структуры :doc:`DocumentSenderSignature <DocumentSenderSignature>`.

	- ``Content`` — подготовленное к подписанию содержимое документа. Формировать подпись нужно для содержимого.

----

.. rubric:: Смотри также

*Структура используется:*
	- в теле ответа метода :doc:`../http/PrepareDocumentsToSign`.
