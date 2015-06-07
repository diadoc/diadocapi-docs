PrepareDocumentsToSignResponse
==============================

.. code-block:: protobuf

    message PrepareDocumentsToSignResponse {
        repeated DocumentPatchedContent DocumentPatchedContents = 1;
    }

    message DocumentPatchedContent {
        required DocumentId DocumentId = 1;
        required string PatchedContentId = 2;
        optional bytes Content = 3;
    }
        

Структура данных PrepareDocumentsToSignResponse представляет документы, подготовленные к подписанию и отправке:

-  DocumentPatchedContents - список документов, подготовленных к подписанию и отправке. Каждый элемент списка представлен структурой типа DocumentPatchedContent.

Структура данных DocumentPatchedContent представляет подготовленное к подписанию содержимое одного документа:

-  DocumentId - идентификатор документа, задаваемый структурой :doc:`DocumentId`, который был подготовлен к подписанию и
   отправке.

-  PatchedContentId - идентификатор содержимого документа, подготовленного к подписанию и отправке. Этот идентификатор можно использовать при вызове метода :doc:`../http/SendDraft` в структуре :doc:`DocumentSenderSignature <DocumentSenderSignature>` в поле PatchedContentId.

-  Content - подготовленное к подписанию содержимое документа. Формировать подпись необходимо именно для этого содержимого.