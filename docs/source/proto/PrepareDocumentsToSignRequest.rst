PrepareDocumentsToSignRequest
=============================

.. code-block:: protobuf

    message PrepareDocumentsToSignRequest {
        required string BoxId = 1;
        repeated DraftDocumentToPatch DraftDocuments = 2;
    }

    message DraftDocumentToPatch {
        required DocumentId DocumentId = 1;
        optional string ToBoxId = 2;
        optional Invoicing.Signer Signer = 3;
    }
        

Структура данных PrepareDocumentsToSignRequest представляет запрос на подготовку документов к подписанию:

-  BoxId - идентификатор ящика, документы которого надо подготовить к подписанию.

-  DraftDocuments - список черновиков документов, которые надо подготовить к подписанию и отправке (отправить их можно с помощью метода :doc:`../http/SendDraft`). Каждый элемент списка представлен структурой типа DraftDocumentToPatch.

Структура данных DraftDocumentToPatch представляет ссылку на черновик документа в Диадоке, а также информацию о подписанте:

-  DocumentId - идентификатор черновика документа, задаваемый структурой :doc:`DocumentId`, который надо подготовить к подписанию и отправке.

-  ToBoxId - идентификатор ящика, в чей адрес планируется отправить документ. Если поле не задано, используется идентификатор ящика получателя из черновика.

-  Signer - информация о подписанте документа, задаваемая структурой :doc:`Signer`. Если поле Signer не задано, подписантом считается сам пользователь, делающий вызов, т.е. будет использовано его ФИО и должность.